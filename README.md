# Blog Example

[template] Microsoft CSS Japan example blog repository.

## Getting Started

[Getting Started](./docs/getting-started.md)

## Init / Update blog theme

https://github.com/jpazureid/hexo-theme-jpazure

```shell
git submodule update -i
```

## Start / Stop Hexo server (local-preview)

```shell
docker-compose up

# Ctrl+C
docker-compose down
```

## Directory structure

```
example
├── .github
│   └── workflows      # Workflows for GitHub Actions
│       └── upload-gh-pages.yml
├── .gitignore
├── .textlintrc
├── README.md
├── _config.yml        # Site configration
├── articles           # Blog articles
│   └── information
│       └── test.md    # Example post
├── docker-compose.yaml    # Configuration for containers (local-preview)
├── docs               # Documents
├── github-issue-template.md
├── scaffolds
├── source
└── themes             # Blog themes
    └── jpazure (git submodule)
```
