<template>
  <div>
    <heading heading="Privacy Policy" subheading="Your privacy matters" />
    <h2>The short version</h2>
    <p>
      This website automatically collects your IP address, your user agent, the
      URL of the page that referred you to this website, and anonymous usage
      data.
    </p>
    <p>
      This website also collects data that you provide (e.g. your email address
      if you include it in the feedback form).
    </p>
    <p>
      Aside: Want to make it harder for websites to track your IP address? Check
      out <a href="https://tails.boum.org/">Tails</a>.
    </p>
    <h2>External links</h2>
    <p>
      This website contains links to external websites. This privacy policy only
      applies to this website, not external websites.
    </p>
    <h2>Data collected by third parties</h2>
    <p>
      This website uses the following third-party services: Netlify Edge, Cloud
      Firestore.
    </p>
    <h3>Netlify Edge</h3>
    <p>
      When you load a page on this website, Netlify Edge stores the following
      information for 30 days:
    </p>
    <ul>
      <li>The URL of the page loaded</li>
      <li>Your IP address</li>
      <li>
        Your user agent (usually contains browser and operating system versions)
      </li>
      <li>The URL of the previous page, if your browser sends it</li>
    </ul>
    <p>
      Netlify Edge is subject to
      <a href="https://www.netlify.com/privacy">Netlify's Privacy Policy</a>.
    </p>
    <h3>Cloud Firestore</h3>
    <p>
      Cloud Firestore stores data collected directly by this website and does
      not collect any additional data.
    </p>
    <p>
      Cloud Firestore is subject to
      <a href="https://policies.google.com/privacy">Google's Privacy Policy</a>.
    </p>
    <h2>Data collected directly by this website</h2>
    <h3>Data automatically collected</h3>
    <p>
      This website automatically collects the following anonymous usage data:
    </p>
    <ul>
      <li>
        When a page is loaded, this website stores:
        <ul>
          <li>The date (in UTC) the page was loaded</li>
          <li>Which page was loaded</li>
        </ul>
      </li>
      <li>
        When a link or button is clicked on this website, this website stores:
        <ul>
          <li>The date (in UTC) the link was clicked</li>
          <li>Which link was clicked</li>
        </ul>
      </li>
      <li>
        When a QR code is scanned on one of our posters to access this website,
        this website stores:
        <ul>
          <li>The date (in UTC) the QR code was scanned</li>
          <li>
            The unique identifier of the QR code
            <ul>
              <li>
                This unique identifier is associated with the geographic
                coordinates where the poster was placed
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
    <h3>Data that you provide</h3>
    <p>
      Data that is submitted via the feedback form is stored indefinitely. If
      you wish to delete data sent via the feedback form, send an email to
      <a href="mailto:contact@valueourminds.com">contact@valueourminds.com</a>
      with the subject line "Delete feedback response" from the email address
      you used to submit the form.
    </p>
    <h2>Contact</h2>
    <p>
      If you have any questions about this privacy policy, please send an email
      to
      <a href="mailto:contact@valueourminds.com">contact@valueourminds.com</a>.
    </p>
  </div>
</template>

<script>
export default {
  head: {
    title: 'Privacy Policy | Value Our Minds',
  },
}
</script>
