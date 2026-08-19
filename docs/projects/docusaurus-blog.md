# Docusaurus Blog

<!--INSERT YOUR BRIEF DESCRIPTION HERE -->
My personal developer blog for documenting my journey through DevSecOps, including what I learn, build, and experiment with along the way.

## Table of Contents

<!--INSERT YOUR TABLE OF CONTENTS HERE -->

- [Quickstart](#quickstart)
- [Description](#description)
- [Further References](#further-references)

import GithubLinkAdmonition from '@site/src/components/GithubLinkAdmonition';

<GithubLinkAdmonition 
    link="https://github.com/DaveHannemann/my-dso-blog"
    title="Github Tip" 
    type="tip"
>
Checkout this repository to see the code/implementation
</GithubLinkAdmonition>

## Quickstart

1. Clone the repository:

   ```bash
   git clone git@github.com:DaveHannemann/my-dso-blog.git
   cd my-dso-blog
   ```

2. Create a .env file based on the provided example.env and configure the required environment variables.

3. Install the dependencies:

    ```bash
    pnpm install
    ```

4. Start the local development server:

    ```bash
    pnpm start
    ```

5. Open the displayed local URL in your browser to view the website.

## Description

This project is a personal developer blog built with Docusaurus. It is used as a learning diary to document my DevSecOps journey, including projects, technical topics, and lessons learned.

The original Docusaurus starter has been adapted to fit the project's structure and purpose. The Docusaurus configuration was customized for the blog, GitHub repository integration, navigation, footer, and environment-based configuration.

The README and deployment documentation were also adapted to describe the project's current workflow. The website is automatically deployed to GitHub Pages through a prepared GitHub Actions workflow whenever a commit is pushed to the main branch.

## Further References

- [Docusaurus Documentation](https://docusaurus.io/docs)
- [Docusaurus Deployment](https://docusaurus.io/docs/deployment)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)