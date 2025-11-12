# Spatial Data & GIS Educational Platform

> An open educational resource for Geographic Information Systems and spatial analysis at TU Delft's Department of Urbanism.

[![Website](https://img.shields.io/badge/website-live-brightgreen)](https://sdgis-edu-tud.github.io/) [![License](https://img.shields.io/badge/license-CC--BY--4.0-blue.svg)](LICENSE) [![Quarto](https://img.shields.io/badge/Made%20with-Quarto-75AADB.svg)](https://quarto.org)

## 📖 About

The Spatial Data & GIS Platform provides comprehensive educational resources for students and educators in the Faculty of Architecture and the Built Environment at TU Delft. The platform includes tutorials, datasets, tools, and collaborative learning materials for both Bachelor's and Master's programs.

**Live site:** <https://sdgis-edu-tud.github.io/>

## ✨ Features

-   🗺️ **GIS Tutorials** - Step-by-step guides for QGIS, from basics to advanced analysis
-   📊 **R for Spatial Analysis** - Geospatial data processing with R
-   🛠️ **Software & Tools** - Curated list of open-source GIS software
-   📍 **Data Sources** - Guide to finding spatial datasets for the Netherlands and beyond
-   🎓 **Course Materials** - Resources for MSc Urbanism workshops and courses
-   🤝 **Open & Collaborative** - Community-driven content development

## 🚀 Quick Start

### For Users

Simply visit the [live website](https://sdgis-edu-tud.github.io/) to access all tutorials and resources.

### For Contributors

1.  **Clone the repository**

    ``` bash
    git clone https://github.com/sdgis-edu-tud/sdgis-edu-tud.github.io.git
    cd your-repo
    ```

2.  **Install Quarto**

    -   Download from [quarto.org](https://quarto.org/docs/get-started/)

    -   Or install via package manager:

        ``` bash
        # macOS
        brew install quarto

        # Windows (with Chocolatey)
        choco install quarto
        ```

3.  **Preview the site locally**

    ``` bash
    quarto preview
    ```

    The site will open at `http://localhost:4200`

4.  **Build the site**

    ``` bash
    quarto render
    ```

## 📂 Repository Structure

```         
.
├── _quarto.yml           # Main configuration file
├── index.qmd             # Homepage
├── styles.css            # Custom styling
├── pages/                # Main content pages
│   ├── installation_setup/
│   ├── getting_started.qmd
│   ├── cartography_and_mapping/
│   ├── density_analysis/
│   ├── landscape_analysis/
│   ├── software_and_tools.qmd
│   ├── find_data.qmd
│   └── about.qmd
├── courses/              # Course-specific materials
├── images/               # Images and figures
└── docs/                 # Generated site (output-dir)
```

## 🤝 Contributing

We welcome contributions from educators, researchers, and students! Here's how you can help:

### Ways to Contribute

-   📝 **Add tutorials** - Share your GIS teaching materials
-   🐛 **Report issues** - Found a bug or broken link? [Open an issue](https://github.com/your-username/your-repo/issues)
-   💡 **Suggest improvements** - Ideas for new content or features
-   🔧 **Fix errors** - Submit pull requests for typos, code fixes, or updates
-   📊 **Share datasets** - Add links to useful spatial data sources

### Contribution Workflow

1.  Fork the repository
2.  Create a new branch (`git checkout -b feature/new-tutorial`)
3.  Make your changes
4.  Test locally with `quarto preview`
5.  Commit your changes (`git commit -m 'Add tutorial on network analysis'`)
6.  Push to your branch (`git push origin feature/new-tutorial`)
7.  Open a Pull Request

**Contribution Guidelines:** See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed instructions.

## 📝 Content Guidelines

When adding new content:

-   Use clear, concise language appropriate for students
-   Include screenshots and examples where helpful
-   Follow the existing file structure and naming conventions
-   Add proper YAML frontmatter to new `.qmd` files
-   Test all code examples and workflows
-   Cite data sources and external resources

### Adding a New Tutorial

1.  Create a new `.qmd` file in the appropriate `pages/` subdirectory

2.  Add YAML frontmatter:

    ``` yaml
    ---
    title: "Your Tutorial Title"
    ---
    ```

3.  Add the file to `_quarto.yml` sidebar navigation

4.  Preview and test locally

5.  Submit a pull request

## 🛠️ Technical Details

-   **Built with:** [Quarto](https://quarto.org) - Open-source scientific and technical publishing system
-   **Hosted on:** GitHub Pages
-   **Themes:** Cosmo (light) / Slate (dark)
-   **Languages:** Markdown, YAML, CSS

### Key Dependencies

-   Quarto \>= 1.3
-   R (optional, for R tutorials)
-   QGIS (for following GIS tutorials)

## 📄 License

This project is licensed under the [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) (CC BY 4.0).

You are free to: - **Share** - Copy and redistribute the material - **Adapt** - Remix, transform, and build upon the material

Under the following terms: - **Attribution** - Give appropriate credit to TU Delft Department of Urbanism

## 👥 Team

**Maintainers:**
- [Daniele Cannatella](https://github.com/dcannatella/) - Department of Urbanism, TU Delft
- [Claudiu Forgaci](https://github.com/cforgaci) - Department of Urbanism, TU Delft
- [Stepan Prikazcicov]() - Department of Urbanism, TU Delft

**Contributors:** See [CONTRIBUTORS.md](CONTRIBUTORS.md)

## 📬 Contact

-   **Email:** SDGIS-BK\@tudelft.nl
-   **Issues:** [GitHub Issues](https://github.com/your-username/your-repo/issues)
-   **Department:** [TU Delft Urbanism](https://www.tudelft.nl/en/architecture-and-the-built-environment/about-the-faculty/departments/urbanism)

## 🙏 Acknowledgments

-   TU Delft Department of Urbanism
-   Faculty of Architecture and the Built Environment
-   All contributors and educators who have shared their materials
-   The Quarto development team
-   The open-source GIS community

------------------------------------------------------------------------

**⭐ If you find this resource helpful, please consider starring the repository!**

Made with ❤️ by the TU Delft Urbanism Spatial Data and GIS team!
