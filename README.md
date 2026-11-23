<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About/Contact | Jennifer's Portfolio</title>
  <link rel="stylesheet" href="./style.css">
</head>
<body>
  <header>
    <h1>About Me</h1>
    <nav aria-label="Main navigation">
      <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="projects.html">Projects/Work</a></li>
        <li><a href="about.html" aria-current="page">About/Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section>
      <h2>About Me</h2>
      <p>I am an Information Technology student learning about web development.</p>
    </section>

    <section>
      <h2>Contact</h2>
      <p>Fields marked required must be completed.</p>

      <form id="contact-form" novalidate>
        <fieldset>
          <legend>Send me a message</legend>

          <div>
            <label for="name">Name (required)</label>
            <input id="name" name="name" type="text"
                   autocomplete="name" required
                   aria-describedby="name-error">
            <span id="name-error" class="form-error" aria-live="polite"></span>
          </div>

          <div>
            <label for="email">Email address (required)</label>
            <input id="email" name="email" type="email"
                   autocomplete="email" required
                   aria-describedby="email-error">
            <span id="email-error" class="form-error" aria-live="polite"></span>
          </div>

          <div>
            <label for="message">Message (required)</label>
            <textarea id="message" name="message" rows="5" required
                      aria-describedby="message-error"></textarea>
            <span id="message-error" class="form-error" aria-live="polite"></span>
          </div>

          <button type="submit">Check message</button>
          <p id="form-status" role="status" aria-live="polite"></p>
        </fieldset>
      </form>
    </section>
  </main>

  <footer>
    <p>Created by Jennifer Natale</p>
  </footer>

  <script>
    const form = document.querySelector("#contact-form");
    const fields = [
      document.querySelector("#name"),
      document.querySelector("#email"),
      document.querySelector("#message")
    ];

    function checkField(field) {
      const error = document.querySelector(`#${field.id}-error`);
      field.removeAttribute("aria-invalid");

      if (field.validity.valueMissing) {
        error.textContent = "Please complete this required field.";
        field.setAttribute("aria-invalid", "true");
        return false;
      }

      if (field.validity.typeMismatch) {
        error.textContent = "Enter a valid email address, such as name@example.com.";
        field.setAttribute("aria-invalid", "true");
        return false;
      }

      error.textContent = "";
      return true;
    }

    fields.forEach((field) => {
      field.addEventListener("input", () => checkField(field));
    });

    form.addEventListener("submit", (event) => {
      event.preventDefault();
      const results = fields.map(checkField);
      const firstInvalid = fields[results.indexOf(false)];

      if (firstInvalid) {
        document.querySelector("#form-status").textContent =
          "Please fix the highlighted fields.";
        firstInvalid.focus();
      } else {
        document.querySelector("#form-status").textContent =
          "All fields are complete. This demo form does not send messages.";
      }
    });
  </script>
</body>
</html>
