
<!-- excerpt from /_includes/masthead.html -->
<header class="masthead">
  <div class="container">
    <a class="masthead__title" href="https://kdboller.github.io">Welcome to Kevin Boller's personal website.</a>
    <nav id="nav-primary" class="masthead__menu-wrapper">
      <ul class="masthead__menu">
        <li><a href="https://kdboller.github.io" class="masthead__menu-item">← Home</a></li>
        {% for link in site.data.navigation.masthead %}
          <li><a href="{{ site.url }}{{ link.url }}" class="masthead__menu-item">{{ link.title }}</a></li>
        {% endfor %}
        <li><a href="#0" class="overlay__menu-trigger masthead__menu-item" aria-label="Navigation Menu" title="Navigation Menu">•&nbsp;•&nbsp;•</a></li>
      </ul>
    </nav>
  </div>
</header>
