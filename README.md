<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>New User Form</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 30px;
      background-color: #f4f4f9;
    }
    h2 {
      color: #333;
      border-bottom: 2px solid #ccc;
      padding-bottom: 5px;
    }
    label {
      display: block;
      margin-top: 10px;
      font-weight: bold;
    }
    input, select, textarea {
      margin-top: 4px;
      padding: 6px;
      width: 300px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    .block {
      background-color: white;
      border-radius: 10px;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
      padding: 20px;
      margin-bottom: 25px;
    }
    .warning {
      color: red;
      font-size: 0.9em;
    }
    .slider-value {
      font-weight: bold;
      margin-left: 10px;
    }
    button {
      background-color: #007bff;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>

  <h1>New User Form</h1>

  <!-- Block 1: Personal Info -->
  <div class="block">
    <h2>Block/Area 1: Personal Info</h2>

    <label>First Name</label>
    <input type="text" name="firstName" pattern="[A-Za-z'-]{1,30}" required />

    <label>Middle Initial</label>
    <input type="text" name="middleInitial" pattern="[A-Za-z]{0,1}" />

    <label>Last Name</label>
    <input type="text" name="lastName" pattern="[A-Za-z0-9'-]{1,30}" required />

    <label>Birth Date</label>
    <input type="date" id="birthDate" name="birthDate" required />

    <label>ID # (Password Style)</label>
    <input type="password" name="idNumber" minlength="5" maxlength="20" />
  </div>

  <!-- Block 2: Contact Info -->
  <div class="block">
    <h2>Block/Area 2: Contact Info</h2>

    <label>Email</label>
    <input type="email" name="email" placeholder="name@domain.com" required />

    <label>Phone Number</label>
    <input type="tel" name="phone" pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}" placeholder="000-000-0000" required />
  </div>

  <!-- Block 3: Address -->
  <div class="block">
    <h2>Block/Area 3: Address</h2>

    <label>Address Line 1</label>
    <input type="text" name="address1" minlength="2" maxlength="30" required />

    <label>Address Line 2</label>
    <input type="text" name="address2" minlength="2" maxlength="30" />

    <label>City</label>
    <input type="text" name="city" minlength="2" maxlength="30" required />

    <label>State</label>
    <select name="state" required>
      <option value="">-- Select State --</option>
      <option value="AL">AL</option><option value="AK">AK</option>
      <option value="AZ">AZ</option><option value="AR">AR</option>
      <option value="CA">CA</option><option value="CO">CO</option>
      <option value="CT">CT</option><option value="DE">DE</option>
      <option value="DC">DC</option><option value="FL">FL</option>
      <option value="GA">GA</option><option value="HI">HI</option>
      <option value="ID">ID</option><option value="IL">IL</option>
      <option value="IN">IN</option><option value="IA">IA</option>
      <option value="KS">KS</option><option value="KY">KY</option>
      <option value="LA">LA</option><option value="ME">ME</option>
      <option value="MD">MD</option><option value="MA">MA</option>
      <option value="MI">MI</option><option value="MN">MN</option>
      <option value="MS">MS</option><option value="MO">MO</option>
      <option value="MT">MT</option><option value="NE">NE</option>
      <option value="NV">NV</option><option value="NH">NH</option>
      <option value="NJ">NJ</option><option value="NM">NM</option>
      <option value="NY">NY</option><option value="NC">NC</option>
      <option value="ND">ND</option><option value="OH">OH</option>
      <option value="OK">OK</option><option value="OR">OR</option>
      <option value="PA">PA</option><option value="PR">PR</option>
      <option value="RI">RI</option><option value="SC">SC</option>
      <option value="SD">SD</option><option value="TN">TN</option>
      <option value="TX">TX</option><option value="UT">UT</option>
      <option value="VT">VT</option><option value="VA">VA</option>
      <option value="WA">WA</option><option value="WV">WV</option>
      <option value="WI">WI</option><option value="WY">WY</option>
    </select>

    <label>Zip Code</label>
    <input type="text" name="zip" pattern="^\d{5}(-\d{4})?$" required placeholder="77002 or 77002-1234" />
  </div>

  <!-- Block 4: Choices -->
  <div class="block">
    <h2>Block/Area 4: Choices</h2>

    <label>Check all that apply:</label>
    <input type="checkbox" /> Chicken Pox
    <input type="checkbox" /> Measles
    <input type="checkbox" /> Covid-19
    <input type="checkbox" /> Flu
    <input type="checkbox" /> Other

    <label>Do you own or rent?</label>
    <input type="radio" name="housing" value="own" /> Own
    <input type="radio" name="housing" value="rent" /> Rent
    <input type="radio" name="housing" value="unsure" /> Unsure

    <label>Desired Salary</label>
    <input type="range" id="salary" min="20000" max="200000" step="1000" value="60000" oninput="updateSalaryValue(this.value)" />
    <span id="salaryValue" class="slider-value">$60,000</span>

    <label>Comments</label>
    <textarea name="comments" rows="4" cols="40" placeholder="Optional..."></textarea>

    <label>Desired User ID</label>
    <input type="text" id="userID" name="userID" pattern="^[A-Za-z_][A-Za-z0-9_-]{4,29}$" required />

    <label>Password</label>
    <input type="password" id="password" minlength="8" maxlength="30" required />

    <label>Re-enter Password</label>
    <input type="password" id="confirmPassword" minlength="8" maxlength="30" required />

    <p id="passwordWarning" class="warning"></p>
  </div>

  <button type="button" onclick="validateForm()">Submit</button>

  <script>
    // Date validation
    const birthInput = document.getElementById("birthDate");
    const today = new Date();
    const minDate = new Date(today.getFullYear() - 120, today.getMonth(), today.getDate());
    const maxDate = today;
    birthInput.min = minDate.toISOString().split("T")[0];
    birthInput.max = maxDate.toISOString().split("T")[0];

    // Slider
    function updateSalaryValue(val) {
      document.getElementById("salaryValue").textContent = "$" + parseInt(val).toLocaleString();
    }

    // Password validation
    function validateForm() {
      const userID = document.getElementById("userID").value.toLowerCase();
      const password = document.getElementById("password").value;
      const confirmPassword = document.getElementById("confirmPassword").value;
      const warning = document.getElementById("passwordWarning");

      const strongPassword = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#%^&*()\-_=+\\|[\]{};:'<>,.?/~`]).{8,30}$/;

      if (password !== confirmPassword) {
        warning.textContent = "❌ Passwords do not match.";
        return;
      }
      if (!strongPassword.test(password)) {
        warning.textContent = "❌ Password must include upper, lower, number, and special character.";
        return;
      }
      if (password.toLowerCase().includes(userID)) {
        warning.textContent = "❌ Password cannot include your user ID.";
        return;
      }
      warning.textContent = "✅ Password is valid!";
      alert("Form successfully validated!");
    }
  </script>
</body>
</html>
