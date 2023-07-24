<template>
  <div id="footer">
    <footer>
      <div class="container">
        <div>
          <h3>Site Navigation</h3>
          <ul>
            <li><a href="/sitemap.html">Sitemap</a></li>
            <li><a href="#contact">Contact Us</a></li>
          </ul>
        </div>
        <div>
          <h3>About</h3>
          <ul>
            <li><a href="https://github.com/quockhanh09?tab=repositories" target="_blank" rel="noreferrer">The Code</a></li>
            <li><a href="https://github.com/quockhanh09?tab=repositories" target="_blank" rel="noreferrer">More of my Projects</a></li>
          </ul>
        </div>
        <div>
          <h3>Contact Me</h3>
          <ul>
            <li><a href="https://github.com/quockhanh09" target="_blank" rel="noreferrer">GitHub</a></li>
            <li><a href="mailto:ksdz0209@gmail.com">E-Mail</a></li>
          </ul>
        </div>
        <div>
          <p class="copyright">SmartNotePad</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>

import './styles/Responsive.css'
export default {
  name: "Footer",
};
</script>

<style>
#footer {
    width: 100%;
    height: 100px;
}

.container {
    color: white;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
}

.container a {
    color: #ea1538;
    text-decoration: none;
    font-weight: bolder;
}

.container a:hover {
    color: #bc0f2c;
    text-decoration: underline;
}

ul{
        list-style-type: none;
    }
</style>
