
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <header class="site-header">
    <h1>Wolokoso Saving Group</h1>
    <p class="tagline">Join, Save, Grow — with trusted confirmations.</p>
  </header>

  <main class="container">
    <!-- Join Form -->
    <section class="card join-form" aria-labelledby="joinTitle">
      <h2 id="joinTitle">Become a Member</h2>
      <form id="joinForm" autocomplete="off" novalidate>
        <div class="form-row">
          <label for="fullName">Full Name</label>
          <input type="text" id="fullName" name="fullName" placeholder="E.g., Mutuya Abdullah" required />
        </div>

        <div class="form-row">
          <label for="nin">NIN (14 characters, uppercase letters)</label>
          <input type="text" id="nin" name="nin" placeholder="CM0306757BHD3R" pattern="[A-Z0-9]{14}" required />
        </div>

        <div class="form-row">
          <label for="phone">Phone Number</label>
          <input type="tel" id="phone" name="phone" placeholder="+2567..." required />
        </div>

        <div class="form-row">
          <label for="email">Email</label>
          <input type="email" id="email" name="email" placeholder="you@example.com" required />
        </div>

        <div class="form-row">
          <label for="address">Residential Address</label>
          <textarea id="address" name="address" rows="3" placeholder="Your address" required></textarea>
        </div>

        <div class="form-row">
          <label for="amount">Initial Saving Amount (UGX)</label>
          <input type="number" id="amount" name="amount" min="0" step="100" placeholder="10000 For joining" required />
        </div>

        <div class="form-row">
          <label for="photo">Upload Photo (optional)</label>
          <input type="file" id="photo" name="photo" accept="image/*" />
        </div>

        <div class="form-row">
          <img id="photoPreview" src="" alt="Photo preview" style="display:none; max-width: 200px; border-radius:8px; border:1px solid #ddd;" />
        </div>

        <div class="form-row checkbox-row">
          <input type="checkbox" id="agree" required />
          <label for="agree">I agree to the group rules and privacy policy.</label>
        </div>

        <button type="submit" class="btn-submit">Join Group</button>
      </form>

      <div id="formMessage" class="form-message" aria-live="polite"></div>
    </section>

    <!-- Members Preview -->
    <section class="card members-panel" aria-labelledby="membersTitle">
      <h2 id="membersTitle">Current Members (sample)</h2>
      <ul id="memberList" aria-label="Member list"></ul>
    </section>
  </main>

  <footer class="footer">
    <p>Demo: Email delivery requires a backend service. This page demonstrates the UI and flow.</p>
  </footer>

  <script src="scripts.js"></script>
</body>
</html>
<style>
:root {
  --bg: #f7f7fb;
  --card: #ffffff;
  --text: #1f1f1f;
  --muted: #6b7280;
  --primary: #2563eb;
  --success: #16a34a;
  --danger: #dc2626;
  --radius: 12px;
}
* { box-sizing: border-box; }
html, body { margin: 0; padding: 0; height: 100%; background: var(--bg); color: var(--text); font-family: Inter, system-ui, Arial, sans-serif; }

.site-header {
  text-align: center; padding: 28px 16px 12px;
}
.site-header h1 { margin: 0; font-size: 2rem; }
.site-header .tagline { margin: 6px 0 0; color: var(--muted); }

.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  max-width: 1100px;
  padding: 0 20px 40px;
  margin: 0 auto;
}

.card {
  background: var(--card);
  border-radius: var(--radius);
  padding: 20px;
  box-shadow: 0 4px 14px rgba(0,0,0,.05);
  border: 1px solid #eaeaf0;
}

.join-form h2, .members-panel h2 { margin-top: 0; }

.form-row { display: flex; flex-direction: column; gap: 6px; margin-bottom: 12px; }
.form-row label { font-weight: 600; font-size: 0.95rem; }
.form-row input, .form-row textarea {
  padding: 10px 12px;
  border: 1px solid #dcdbe0;
  border-radius: 8px;
  font-size: 1rem;
  background: #fff;
}
.form-row input:focus, .form-row textarea:focus {
  outline: none; border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.15);
}
.checkbox-row { display: flex; align-items: center; gap: 10px; }
.checkbox-row input { width: 18px; height: 18px; }

.btn-submit {
  background: var(--primary);
  color: #fff;
  border: none;
  padding: 12px 16px;
  border-radius: 8px;
  font-size: 1rem;
  cursor: pointer;
}
.btn-submit:hover { background: #1e40af; }

.form-message {
  margin-top: 12px;
  padding: 10px 12px;
  border-radius: 6px;
  display: inline-block;
}
.form-message.success { background: rgba(22, 163, 74, 0.15); color: #1e6b2e; border: 1px solid rgba(22,163,74,.4); }
.form-message.error { background: rgba(239, 68, 68, 0.15); color: #991b1b; border: 1px solid rgba(239,68,68,.4); }

.members-panel ul { padding-left: 20px; margin: 0; max-height: 260px; overflow-y: auto; }
.members-panel li { margin: 6px 0; }
@media (max-width: 900px) {
  .container { grid-template-columns: 1fr; }
}
.footer { text-align: center; padding: 14px; color: var(--muted); font-size: 0.9rem; }

</style>
<script>
<!-- EmailJS -->
<script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>

<script>
(function(){
  emailjs.init("WZkh6TOGm7QQDLgSa"); // 🔴 put your Public Key here
})();

const memberListEl = document.getElementById('memberList');
const joinForm = document.getElementById('joinForm');
const formMessageEl = document.getElementById('formMessage');
const photoInput = document.getElementById('photo');
const photoPreview = document.getElementById('photoPreview');

const seedMembers = [];

function renderMembers() {
  memberListEl.innerHTML = '';
  seedMembers.forEach(m => {
    const li = document.createElement('li');
    li.textContent = `${m.name} (${m.email})`;
    memberListEl.appendChild(li);
  });
}

function showMessage(text, isSuccess) {
  formMessageEl.textContent = text;
  formMessageEl.className = 'form-message ' + (isSuccess ? 'success' : 'error');
}

function validateNIN(nin) {
  return /^[A-Z0-9]{14}$/.test(nin);
}

// Photo preview
photoInput.addEventListener('change', () => {
  const file = photoInput.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      photoPreview.src = e.target.result;
      photoPreview.style.display = 'block';
    };
    reader.readAsDataURL(file);
  }
});

// FORM SUBMIT
joinForm.addEventListener('submit', function(e) {
  e.preventDefault();

  const fullName = document.getElementById('fullName').value.trim();
  const nin = document.getElementById('nin').value.trim().toUpperCase();
  const email = document.getElementById('email').value.trim();
  const phone = document.getElementById('phone').value.trim();
  const address = document.getElementById('address').value.trim();
  const amount = document.getElementById('amount').value;
  const agree = document.getElementById('agree').checked;

  if (!fullName || !nin || !email || !phone || !address || !amount || !agree) {
    showMessage('Fill all fields first.', false);
    return;
  }

  if (!validateNIN(nin)) {
    showMessage('Invalid NIN format.', false);
    return;
  }

  const templateParams = {
    fullName,
    nin,
    email,
    phone,
    address,
    amount
  };

  // 🔥 SEND EMAIL
  emailjs.send(
    "service_y17uayu",   // 🔴 put Service ID
    "template_7pillkf",  // 🔴 put Template ID
    templateParams
  ).then(function(response) {
      showMessage("Member added & email sent successfully!", true);

      seedMembers.push({ name: fullName, email });
      renderMembers();
      joinForm.reset();
      photoPreview.style.display = 'none';

  }, function(error) {
      showMessage("Failed to send email. Check setup.", false);
      console.error(error);
  });
});

renderMembers();
</script>

</script>
