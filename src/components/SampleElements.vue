<template>
  <div class="samples">
    <div class="card center allyCheck">
      <h1>A11y</h1>
      <p>
        This theme has a contrast ratio of {{ contrast }} which makes it
        {{ compliance }}.
      </p>

      <p>
        <a href="#">
          This theme has a link contrast ratio of {{ linkContrast }} which makes
          it {{ linkCompliance }}.
        </a>
      </p>

      <p class="navCheck">
        This theme header has a contrast ratio of {{ navContrast }} which makes it
        {{ navCompliance }}.
      </p>

      <p>
        Learn more about WCAG text contrast compliance
        <a
          href="https://webaim.org/resources/contrastchecker/"
          class="allyLink"
        >here</a>
      </p>
    </div>

    <div class="card">
      <h1>Headers</h1>
      <h1 class="left">This is an h1 tag</h1>
      <h2>This is an h2 tag</h2>
      <h3>This is an h3 tag</h3>
      <h4>This is an h4 tag</h4>
    </div>

    <div class="card center">
      <h1>Tables</h1>
      <table>
        <thead>
          <tr>
            <th>Username</th>
            <th>Age</th>
            <th>Style</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>jSmith</td>
            <td>32</td>
            <td>Primary</td>
          </tr>

          <tr>
            <td>eSmith</td>
            <td>24</td>
            <td>Secondary</td>
          </tr>

          <tr>
            <td>bSmith</td>
            <td>66</td>
            <td>Primary</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="card">
      <h1>Paragraphs</h1>
      <p>This is a sample paragraph. It has one line.</p>
      <p>
        This is also a sample paragraph, but it has more content! There's a
        sentence about dogs. There's a sentence about cats. There's a sentence
        about birds. There's a sentence about fish. There's a sentence about
        pigs. There's a sentence about cows. There's even one about bears!
      </p>
    </div>

    <div class="card">
      <h1>Lists</h1>
      <h2>Unordered Lists</h2>
      <h3>Things I like</h3>
      <ul>
        <li>Themes</li>
        <li>Code</li>
        <li>Coffee</li>
      </ul>

      <h2>Ordered Lists</h2>
      <h3>My Favorite Colors</h3>
      <ol>
        <li>Yellow</li>
        <li>Purple</li>
        <li>Aqua</li>
      </ol>
    </div>

    <div class="card center">
      <h1>Images</h1>
      <img src="/kitten.jpg" alt="picture of a cute cat from pixabay <3"/>
    </div>
    <!--
    <div class="card center">
      <h1>Forms (Inputs)</h1>
      <form>
        <label for="fname">First Name</label>
        <input type="text" id="fname" name="firstname" placeholder="Your name..">
        <br>
        <label for="lname">Last Name</label>
        <input type="text" id="lname" name="lastname" placeholder="Your last name..">
        <br>
        <label for="country">Country</label>
        <select id="country" name="country">
          <option value="australia">Australia</option>
          <option value="canada">Canada</option>
          <option value="usa">USA</option>
        </select>
        <br>
        <label for="subject">Subject</label>
        <textarea id="subject" name="subject" placeholder="Write something.." style="height:200px"></textarea>
        <br>
        <input type="submit" value="Submit">
      </form>
    </div>
    -->
  </div>
</template>

<script>
var luminance = require("relative-luminance").default;
export default {
  name: "SampleElements",
  data: function() {
    return {
      bgLumi: 1,
      colorLumi: 0.021232136932028953,
      linkLumi: 0.1157959368559201,
      navLumi: 0.021232136932028953,
      contrast: 14.74,
      linkContrast: 7.79,
      navContrast: 14.74,
      linkCompliance: "AAA compliant",
      compliance: "AAA compliant",
      navCompliance: "AAA compliant",
      colorArray: [],
      bgArray: [],
      linkArray: [],
      navTextArray: []
    };
  },
  methods: {
    getContrast: function() {
      this.updateLumi();
      let lumi1 = this.colorLumi;
      let lumi2 = this.bgLumi;
      let lumi3 = this.linkLumi;
      let lumi4 = this.navLumi;
      // Calculate Main Contrast Ratio
      this.contrast =
        lumi1 > lumi2
          ? (lumi1 + 0.05) / (lumi2 + 0.05)
          : (lumi2 + 0.05) / (lumi1 + 0.05);
      this.contrast = Math.round(this.contrast * 100) / 100;
      if (this.contrast >= 7) {
        this.compliance = "AAA compliant";
      } else if (this.contrast >= 4.5) {
        this.compliance = "AA compliant";
      } else {
        this.compliance = "not compliant with WCAG";
      }

      // Calculate Link Contrast Ratio
      this.linkContrast =
        lumi3 > lumi2
          ? (lumi3 + 0.05) / (lumi2 + 0.05)
          : (lumi2 + 0.05) / (lumi3 + 0.05);
      this.linkContrast = Math.round(this.linkContrast * 100) / 100;
      if (this.linkContrast >= 7) {
        this.linkCompliance = "AAA compliant";
      } else if (this.linkContrast >= 4.5) {
        this.linkCompliance = "AA compliant";
      } else {
        this.linkCompliance = "not compliant with WCAG";
      }

      // Calculate Navbar Contrast Ratio
      this.navContrast =
        lumi2 > lumi4
          ? (lumi2 + 0.05) / (lumi4 + 0.05)
          : (lumi4 + 0.05) / (lumi2 + 0.05);
      this.navContrast = Math.round(this.navContrast * 100) / 100;
      if (this.navContrast >= 7) {
        this.navCompliance = "AAA compliant";
      } else if (this.navContrast >= 4.5) {
        this.navCompliance = "AA compliant";
      } else {
        this.navCompliance = "not compliant with WCAG";
      }
    },
    updateLumi: function() {
      // Grab colors, use Regex to create Array
      this.colorArray = getComputedStyle(document.querySelector(".allyCheck"))
        .color.replace(/[^\d,]/g, "")
        .split(",");
      this.bgArray = getComputedStyle(document.querySelector(".allyCheck"))
        .backgroundColor.replace(/[^\d,]/g, "")
        .split(",");
      this.linkArray = getComputedStyle(document.querySelector(".allyLink"))
        .color.replace(/[^\d,]/g, "")
        .split(",");
      this.navTextArray = getComputedStyle(document.querySelector(".navCheck"))
        .backgroundColor.replace(/[^\d,]/g, "")
        .split(",");

      // Use Luminance to calculate Luminance (range 0 - 1)
      this.bgLumi = luminance([
        this.bgArray[0],
        this.bgArray[1],
        this.bgArray[2]
      ]);
      this.colorLumi = luminance([
        this.colorArray[0],
        this.colorArray[1],
        this.colorArray[2]
      ]);
      this.linkLumi = luminance([
        this.linkArray[0],
        this.linkArray[1],
        this.linkArray[2]
      ]);

      this.navLumi = luminance([
        this.navTextArray[0],
        this.navTextArray[1],
        this.navTextArray[2]
      ]);
    }
  },
  mounted() {
    // When a new theme is selected, it Emits "themeSelected"
    // When this happens, run .getContrast()
    this.$root.$on("themeSelected", () => {
      this.getContrast();
    });
  }
};
</script>

<style lang="scss" scoped>
.center {
  text-align: center;
}

/* Material Card setup */
.card {
  color: var(--text);
  background-color: var(--secondary);
  border: 3px solid var(--accent);
  width: 50%;
  margin: 10px auto auto;
  border-radius: 17px;
  padding: 10px;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14),
    0 3px 1px -2px rgba(0, 0, 0, 0.12), 0 1px 5px 0 rgba(0, 0, 0, 0.2);

  // Align first h1 tag in each card
  > h1:nth-child(1) {
    text-align: center;
  }
}

/* Table Styling */
table {
  width: 100%;
  border-collapse: collapse;
}

tr:nth-child(even) {
  background-color: var(--primary);
  color: var(--secondary);
}

.navCheck {
  background-color: var(--primary);
  color: var(--secondary);
}
</style>
