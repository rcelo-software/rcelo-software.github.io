## Getting Started

#### Prerequisites

- Docker
- Docker Compose

### Running the Site

#### Production Build

```bash
# Build the site for production
docker-compose run --rm site jekyll build

# The built site will be in the _site directory
# Deploy these files to your web server
```

#### Local Development

```bash
# Start the development server with auto-reload
docker-compose up

# Access the site at http://localhost:4000
```

The development server includes hot-reload functionality:

- Changes to posts, pages, and most content files will trigger automatic rebuild
- Changes to `_config.yml` require a server restart
- Changes to Gemfile or Dockerfile require rebuilding the container:

  ```bash
  docker-compose down
  docker-compose up --build
  ```

### Building the Website

```bash
# Normal build
docker-compose run --rm site jekyll build

# Force rebuild (ignores cache)
docker-compose run --rm site jekyll build --force

# Build with drafts and future posts
docker-compose run --rm site jekyll build --drafts --future

# Build with detailed output
docker-compose run --rm site jekyll build --verbose
```

Common build flags:

- `--drafts`: Include draft posts from `_drafts` folder
- `--future`: Include posts with future dates
- `--force`: Force a rebuild, ignoring cache
- `--verbose`: Output detailed build information
- `--watch`: Watch for changes and rebuild automatically

### Troubleshooting

If changes aren't reflecting:

```bash
# Stop containers and clean up
docker-compose down

# Rebuild and restart
docker-compose up --build
```

## Project Structure

```
.
├── _config.yml          # Site configuration
├── _data/              # Site data files
│   ├── navigation.yml  # Navigation menu configuration
│   └── social.yml      # Social media links
├── _includes/          # Reusable HTML components
│   ├── footer.html     # Site footer template
│   ├── header.html     # Site header template
│   └── head.html       # Document head template
├── _layouts/           # Page layout templates
│   ├── default.html    # Base layout template
│   ├── page.html       # Static page layout
│   └── post.html       # Blog post layout
├── _sass/              # Sass stylesheets
│   ├── base/           # Base styles
│   ├── components/     # Component styles
│   └── main.scss       # Main stylesheet
├── assets/             # Static assets
│   ├── css/           # Compiled CSS
│   ├── images/        # Image files
│   └── js/            # JavaScript files
├── content/            
│   ├── _posts/        # Blog posts directory
│   └── pages/         # Static pages
├── .gitignore         # Git ignore rules
├── Dockerfile         # Container definition
├── docker-compose.yml # Docker compose configuration
├── Gemfile           # Ruby dependencies
└── index.md          # Homepage
```

## Content Management

### Creating Blog Posts

1. Create a new markdown file in `content/_posts` with the naming convention:
   - Format: `YYYY-MM-DD-title.md`
   - Example: `2024-03-20-getting-started-with-docker.md`

2. Add the required front matter at the top of your post:

```yaml
---
layout: post
title: "Your Post Title"
date: YYYY-MM-DD
categories: [category1, category2]
tags: [tag1, tag2]  # Optional
---
```

3. Write your post content in markdown format below the front matter

### Adding Navigation Items

To add new navigation links, edit `_data/navigation.yml`:

```yaml
- title: "Home"
  url: "/"
- title: "About"
  url: "/about/"
```

## Development Notes

### Auto-Reload Behavior

The development server (`docker-compose up`) includes live-reload functionality:

- **Automatic Updates:**
  - Blog posts
  - Pages
  - Assets (CSS, JavaScript, images)
  - Templates and includes
  - Most content files

- **Requires Server Restart:**

  ```bash
  # When changing _config.yml
  docker-compose down
  docker-compose up
  ```

- **Requires Container Rebuild:**

  ```bash
  # When modifying:
  # - Gemfile
  # - Dockerfile
  # - docker-compose.yml
  docker-compose down
  docker-compose up --build
  ```

### Common Issues

1. **Changes not showing up:**
   - Clear your browser cache
   - Check if the file is being watched (see auto-reload list above)
   - Verify file location matches project structure

2. **Server not starting:**
   - Ensure ports are not in use
   - Check Docker logs for errors
   - Verify Docker service is running
