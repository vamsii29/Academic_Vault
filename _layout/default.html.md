<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>{{ page.title }}</title>

    <!-- MathJax for LaTeX rendering -->
    <script type="text/javascript" async
      src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
    </script>

    <!-- Optional: some basic styling -->
    <style>
      body {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
        margin: 2rem;
        line-height: 1.6;
        max-width: 800px;
      }
    </style>
  </head>
  <body>
    <main>
      {{ content }}
    </main>
  </body>
</html>