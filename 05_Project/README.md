<div id="top"></div>

<!-- [![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

[contributors-shield]: https://img.shields.io/github/contributors/kiran-karandikar/repo_name?style=for-the-badge

[contributors-url]: https://github.com/Kiran-Karandikar/repo_name/graphs/contributors

[forks-shield]: https://img.shields.io/github/forks/Kiran-Karandikar/repo_name?style=for-the-badge

[forks-url]: https://github.com/Kiran-Karandikar/repo_name/network

[stars-shield]: https://img.shields.io/github/stars/Kiran-Karandikar/repo_name?style=for-the-badge

[stars-url]: https://github.com/Kiran-Karandikar/repo_name/stargazers

[issues-shield]: https://img.shields.io/github/issues/Kiran-Karandikar/repo_name?style=for-the-badge

[issues-url]: https://github.com/Kiran-Karandikar/repo_name/issues

[license-shield]: https://img.shields.io/github/license/Kiran-Karandikar/repo_name?style=for-the-badge

[license-url]: https://github.com/Kiran-Karandikar/repo_name/blob/master/LICENSE

[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555

[linkedin-url]: https://linkedin.com/in/kiran-karandikar -->

<!-- --------- -->

<!-- PROJECT LOGO -->
<br />
<div align="center">
<h3 align="center">Spam message Classifier for Hindi Language.</h3>
  <p align="center">
    Supervised machine learning for natural language processing to classify spam messages for Hindi Language.
    <br />
    <!-- <a href="https://kiran-karandikar.github.io/repo_name"><strong>Preview</strong></a>
    <br />
    <a href="https://github.com/kiran-karandikar/repo_name"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/kiran-karandikar/repo_name">View Demo</a>
    ·
    <a href="https://github.com/kiran-karandikar/repo_name/issues">Report Bug</a>
    ·
    <a href="https://github.com/kiran-karandikar/repo_name/issues">Request Feature</a> -->
  </p>
</div>

<!-- BADGES.MD Finish -->

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
        <li><a href="#data-description">Data Description</a></li>
      </ul>
    </li>
    <!-- <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li> -->
    <!-- <li><a href="#usage">Usage</a></li> -->
    <!-- <li><a href="#roadmap">Roadmap</a></li> -->
    <li><a href="#license">License</a></li>
    <!-- <li><a href="#contact">Contact</a></li> -->
    <!-- <li><a href="#acknowledgments">Acknowledgments</a></li> -->
  </ol>
</details>

<!-- ABOUT THE PROJECT -->

## About The Project

In recent times, there has been an increase in spam messages that contain regional Indian languages, in particular Hindi. However, there are limited resources that have classification of Hindi language. This is even though Hindi is a widely spoken language not only in India but also around the world; it is the 4th most spoken language across the world.  As such, this premise presented me with the need for an automatic text-classifier, in order to create a text classifier for Hindi Spam messages. Thus, in the present work, I use supervised learning methods using Naive Bayes Classifier and Ontology-based classification to facilitate text classification for Hindi Text and enable the identification for Hindi Spam messages. Doing so, I hope to contribute towards improved spam messages filtration when the text is in Hindi, and thus reduce the risk posed by spam messages.

<p align="right">(<a href="#top">back to top</a>)</p>

### Built With

* [scikit-learn](https://scikit-learn.org/stable/index.html)
* [nltk](https://www.nltk.org/)
* [inltk](https://inltk.readthedocs.io/en/latest/index.html)
* [indic-nlp-library](https://anoopkunchukuttan.github.io/indic_nlp_library/)
* [ai4bharat](https://github.com/AI4Bharat/indic-bert)
* [Google Colab](https://colab.research.google.com)

<p align="right">(<a href="#top">back to top</a>)</p>

### Data Description

* [`Data/hindi_sms_data.csv`](./Data/hindi_sms_data.csv):
  * The [UCI SMS spam collection dataset](https://archive.ics.uci.edu/ml/datasets/SMS+Spam+Collection) was used for this project. The SMS Spam Collection is a collection of SMS-tagged messages gathered for SMS Spam research. It contains one set of 5,574 SMS messages in English that have been classified as ham (legitimate) or spam.
  * The UCI SMS dataset is entirely in English. Thus, The [Google Translate service](https://translate.google.com/?sl=en&tl=hi&op=docs.) was used to translate the English words and sentences into the appropriate Hindi sentences.
* [```Data/historical_experiments_log.csv```](./Data/historical_experiments_log.csv):
  * Log information for experimental features and model Hyperparameter tuning.
* [```Data/grid_search_logs.csv```](./Data/grid_search_logs.csv):
  * Log data for the most recent grid search run.

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- GETTING STARTED -->
<!-- 
## Getting Started

This is an example of how you may give instructions on setting up your project
locally.
To get a local copy up and running follow these simple example steps.

### Prerequisites

This is an example of how to list things you need to use the software and how to
install them.

* npm

  ```sh
  npm install npm@latest -g
  ``` -->

<!-- ### Installation

1. Clone the repo

   ```sh
   git clone https://github.com/kiran-karandikar/repo_name.git
   ```

2. Additional Steps here...

<p align="right">(<a href="#top">back to top</a>)</p> -->

<!-- USAGE EXAMPLES -->
<!-- 
## Usage

Use this space to show useful examples of how a project can be used. Additional
screenshots, code examples and demos work well in this space. You may also link
to more resources.

_For more examples, please refer to the [Documentation](https://example.com)_

<p align="right">(<a href="#top">back to top</a>)</p> -->

<!-- ROADMAP 

## Roadmap

- [ ] Feature 1
- [ ] Feature 2
- [ ] Feature 3
	- [ ] Nested Feature

See the [open issues](https://github.com/kiran-karandikar/repo_name/issues) for a
full list of proposed features (and known issues).

<p align="right">(<a href="#top">back to top</a>)</p>
-->

<!-- LICENSE -->

## License

Distributed under the `MIT License`. See `LICENSE` for more information.

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- ACKNOWLEDGMENTS -->

<!-- ## Acknowledgments

* []()
* []()
* []()

<p align="right">(<a href="#top">back to top</a>)</p> -->

<!-- MARKDOWN LINKS & IMAGES -->

<!-- CONTACT -->

<!-- ## Contact

* [Kiran Karandikar](mailto:khkarandikar@gmail.com) -->

<!-- Project
Link: [https://github.com/kiran-karandikar/repo_name](https://github.com/kiran-karandikar/repo_name) -->

<!-- <p align="right">(<a href="#top">back to top</a>)</p> -->
