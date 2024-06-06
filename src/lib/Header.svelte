<header class="full-width">
  <h1>TV Archive</h1>
  <div class="input">
    <p>⌕</p>
    <input type="text" placeholder="Search" />
  </div>
</header>

<style lang="scss">
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 80px;
    border-bottom: 1px solid rgba(#6f5643, 0.25);
    padding-inline: 120px;
  }

  .input {
    display: flex;
    max-width: 200px;
    background-color: #dcd5ae;
    border: none;
    border-radius: 1000px;
    padding: 0.25rem 1rem;

    & p {
      font-size: 1.25rem;
      margin: 0;
    }

    & input {
      background: none;
      border: none;
      outline: none;
      color: inherit;
      width: 100%;
      margin-left: 0.5rem;
    }
  }
</style>
