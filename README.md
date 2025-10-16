<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Comprehensive Form — Validation Demo</title>
<style>
  :root{font-family:Inter,system-ui,Arial,sans-serif;--err:#b00020;--ok:#006600}
  body{max-width:900px;margin:28px auto;padding:18px;background:#f7f8fb;border-radius:10px}
  h1{margin-top:0}
  fieldset{border:1px solid #ddd;padding:14px;margin-bottom:16px;border-radius:8px;background:white}
  .row{display:flex;gap:12px;flex-wrap:wrap}
  .col{flex:1 1 220px;min-width:180px}
  label{display:block;font-weight:600;margin-bottom:6px}
  input[type="text"],input[type="email"],input[type="password"],input[type="date"],select,textarea{
    width:100%;padding:8px;border:1px solid #bbb;border-radius:6px;font-size:14px;box-sizing:border-box
  }
  .inline-help{font-size:12px;color:#666;margin-top:4px}
  .error{color:var(--err);font-size:13px;margin-top:6px}
  .ok{color:var(--ok);font-size:13px;margin-top:6px}
  .small{font-size:13px;color:#444}
  .checkbox-grid{display:flex;flex-wrap:wrap;gap:8px}
  .checkbox-grid label{display:inline-flex;align-items:center;gap:6px;font-weight:400}
  .radio-row{display:flex;gap:12px;align-items:center}
  .slider-row{display:flex;align-items:center;gap:12px}
  .value-box{min-width:140px;text-align:right;font-weight:700}
  button{background:#2563eb;color:white;padding:10px 16px;border:0;border-radius:8px;font-weight:700;cursor:pointer}
  button:disabled{opacity:.6;cursor:not-allowed}
  .field-note{font-size:12px;color:#666;margin-top:4px}
  .msg{padding:8px;border-radius:6px;margin-bottom:12px}
  .msg.err{background:#ffeeef;border:1px solid #ffd3d6;color:#800}
  .msg.ok{background:#eefbf1;border:1px solid #b9e6c5;color:#065}
  textarea{min-height:90px;resize:vertical}
</style>
</head>
<body>
<h1>Demo Form — Validations & Dynamic Behavior</h1>
<div class="small">Page date/time: <span id="pageDate"></span></div>

<form id="mainForm" novalidate>

  <!-- BLOCK / AREA 1: Names, Dates, SSN/ID -->
  <fieldset>
    <legend><strong>Block / Area 1 — Identity & Dates</strong></legend>

    <div class="row">
      <div class="col">
        <label for="firstName">First Name</label>
        <input id="firstName" name="firstName" type="text" required
               pattern="^[A-Za-z'\\-]{1,30}$"
               title="1–30 characters; letters, apostrophes and dashes only">
        <div class="inline-help">1–30 chars. Letters, apostrophes and dashes only.</div>
        <div class="error" id="firstNameErr"></div>
      </div>

      <div class="col">
        <label for="middleInitial">Middle Initial</label>
        <input id="middleInitial" name="middleInitial" type="text"
               pattern="^[A-Za-z]{0,1}$"
               maxlength="1" title="Optional. 1 letter or blank">
        <div class="inline-help">Optional. 1 letter (A–Z) or leave blank.</div>
        <div class="error" id="middleInitialErr"></div>
      </div>

      <div class="col">
        <label for="lastName">Last Name</label>
        <input id="lastName" name="lastName" type="text" required
               pattern="^[A-Za-z'\\-2-5]{1,30}$"
               title="1–30 chars; letters, apostrophes, dashes, digits 2-5 allowed">
        <div class="inline-help">1–30 chars. Letters, apostrophes, dashes, and digits 2–5 allowed.</div>
        <div class="error" id="lastNameErr"></div>
      </div>
    </div>

    <hr style="margin:12px 0">

    <div class="row">
      <div class="col">
        <label for="birthDate">Birth Date (MM/DD/YYYY)</label>
        <input id="birthDate" name="birthDate" type="date" required>
        <div class="field-note">Birthdate must not be in the future and not more than 120 years ago.</div>
        <div class="error" id="birthDateErr"></div>
      </div>

      <div class="col">
        <label for="moveInDate">Move-in Date (MM/DD/YYYY)</label>
        <input id="moveInDate" name="moveInDate" type="date" required>
        <div class="field-note">Move-in date cannot be in the past.</div>
        <div class="error" id="moveInDateErr"></div>
      </div>

      <div class="col">
        <label for="travelDate">Travel Date (MM/DD/YYYY)</label>
        <input id="travelDate" name="travelDate" type="date" required>
        <div class="field-note">Travel date cannot be in the past.</div>
        <div class="error" id="travelDateErr"></div>
      </div>
    </div>

    <hr style="margin:12px 0">

    <div class="row">
      <div class="col">
        <label for="ssn">Social Security (optional) — obscured</label>
        <input id="ssn" name="ssn" type="password" inputmode="numeric"
               pattern="^[0-9]{3}-[0-9]{2}-[0-9]{4}$"
               placeholder="123-45-6789"
               title="Format: 123-45-6789 (optional)">
        <div class="inline-help">Optional. Format: 123-45-6789. This field is obscured like a password.</div>
        <div class="error" id="ssnErr"></div>
      </div>

      <div class="col">
        <label for="idNumber">ID # (required) — obscured</label>
        <input id="idNumber" name="idNumber" type="password" required
               title="This ID is a password-style field (obscured).">
        <div class="inline-help">Please enter your ID number (kept hidden on screen).</div>
        <div class="error" id="idNumberErr"></div>
      </div>
    </div>

  </fieldset>

  <!-- BLOCK / AREA 2: Contact Info -->
  <fieldset>
    <legend><strong>Block / Area 2 — Contact Info</strong></legend>

    <div class="row">
      <div class="col">
        <label for="email">Email address</label>
        <input id="email" name="email" type="email" required
               pattern="^[^@\\s]+@[^@\\s]+\\.[^@\\s]+$"
               title="Must be a standard email format like name@domain.tld">
        <div class="inline-help">Format: name@domain.tld</div>
        <div class="error" id="emailErr"></div>
      </div>

      <div class="col">
        <label for="phone">Phone number</label>
        <input id="phone" name="phone" type="text" required
               pattern="^[0-9]{3}-[0-9]{3}-[0-9]{4}$"
               placeholder="000-000-0000"
               title="Format: 000-000-0000">
        <div class="inline-help">Format: 000-000-0000</div>
        <div class="error" id="phoneErr"></div>
      </div>
    </div>
  </fieldset>

  <!-- BLOCK / AREA 3: Address -->
  <fieldset>
    <legend><strong>Block / Area 3 — Address</strong></legend>

    <div class="row">
      <div class="col">
        <label for="addr1">Address Line 1</label>
        <input id="addr1" name="addr1" type="text" required pattern="^.{2,30}$" title="2–30 characters">
        <div class="inline-help">Required. 2–30 characters.</div>
        <div class="error" id="addr1Err"></div>
      </div>

      <div class="col">
        <label for="addr2">Address Line 2 (optional)</label>
        <input id="addr2" name="addr2" type="text" pattern="^.{2,30}$" title="2–30 characters if provided">
        <div class="inline-help">Optional. If entered, must be 2–30 characters.</div>
        <div class="error" id="addr2Err"></div>
      </div>
    </div>

    <div class="row" style="margin-top:10px">
      <div class="col">
        <label for="city">City</label>
        <input id="city" name="city" type="text" required pattern="^.{2,30}$" title="2–30 characters">
        <div class="inline-help">Required. 2–30 characters.</div>
        <div class="error" id="cityErr"></div>
      </div>

      <div class="col">
        <label for="stateSelect">State</label>
        <select id="stateSelect" name="stateSelect" required>
          <option value="">-- choose a state --</option>
        </select>
        <div class="inline-help">You must choose a state (2-letter code will be used in data).</div>
        <div class="error" id="stateErr"></div>
      </div>

      <div class="col">
        <label for="zip">Zip Code</label>
        <input id="zip" name="zip" type="text" required pattern="^[0-9]{5}(-[0-9]{4})?$" placeholder="77002 or 77002-1234">
        <div class="inline-help">Required. 5 digits or ZIP+4 (e.g. 77002-1234). On submit we will truncate and redisplay first 5 digits.</div>
        <div class="error" id="zipErr"></div>
      </div>
    </div>

  </fieldset>

  <!-- BLOCK / AREA 4: Choices -->
  <fieldset>
    <legend><strong>Block / Area 4 — Choices</strong></legend>

    <div>
      <label>Check all of the following that apply:</label>
      <div class="checkbox-grid" aria-describedby="illnessHelp">
        <label><input type="checkbox" name="illness" value="chickenpox"> Chicken Pox</label>
        <label><input type="checkbox" name="illness" value="measles"> Measles</label>
        <label><input type="checkbox" name="illness" value="covid"> Covid-19</label>
        <label><input type="checkbox" name="illness" value="mumps"> Mumps</label>
        <label><input type="checkbox" name="illness" value="flu"> Influenza</label>
      </div>
      <div id="illnessHelp" class="field-note">Select any that apply.</div>
    </div>

    <hr style="margin:12px 0">

    <div style="margin-bottom:10px">
      <label>Housing status</label>
      <div class="radio-row">
        <label><input type="radio" name="housing" value="own" required> Own</label>
        <label><input type="radio" name="housing" value="rent"> Rent</label>
        <label><input type="radio" name="housing" value="unsure"> Unsure</label>
      </div>
      <div class="error" id="housingErr"></div>
    </div>

    <div style="margin-bottom:10px">
      <label>Have you been vaccinated?</label>
      <div class="radio-row">
        <label><input type="radio" name="vaccinated" value="yes" required> Yes</label>
        <label><input type="radio" name="vaccinated" value="no"> No</label>
        <label><input type="radio" name="vaccinated" value="prefer-not"> Prefer not to say</label>
      </div>
      <div class="error" id="vaccinatedErr"></div>
    </div>

    <hr style="margin:12px 0">

    <div>
      <label for="salaryRange">Desired salary (annual)</label>
      <div class="slider-row">
        <input id="salaryRange" name="salaryRange" type="range" min="20000" max="200000" step="1000" value="60000">
        <div class="value-box" id="salaryValue">$60,000</div>
      </div>
      <div class="field-note">Slide to select desired salary from $20,000 to $200,000. Value updates live.</div>
    </div>

    <hr style="margin:12px 0">

    <div>
      <label for="notes">Notes (optional)</label>
      <textarea id="notes" name="notes" placeholder='Avoid using double quotes (") to prevent issues.'></textarea>
      <div class="inline-help">Optional. Double quotes are discouraged; the form will warn if present.</div>
      <div class="error" id="notesErr"></div>
    </div>
  </fieldset>

  <!-- USER ID & PASSWORD -->
  <fieldset>
    <legend><strong>User ID & Password</strong></legend>

    <div class="row">
      <div class="col">
        <label for="userId">Desired User ID</label>
        <input id="userId" name="userId" type="text" required
               pattern="^(?!\\d)[A-Za-z0-9_-]{5,30}$"
               title="5–30 chars. No special characters except underscore or dash. First character cannot be a number. No spaces.">
        <div class="inline-help">5–30 chars. Letters, numbers, underscore or dash. First char must not be a number. No spaces. Will be converted to lowercase at submit.</div>
        <div class="error" id="userIdErr"></div>
      </div>

      <div class="col">
        <label for="pass1">Password</label>
        <input id="pass1" name="pass1" type="password" required minlength="8" maxlength="30" autocomplete="new-password">
        <div class="inline-help">8–30 characters, at least 1 uppercase, 1 lowercase, 1 digit, and 1 special character. Double quotes (") not allowed.</div>
        <div class="error" id="pass1Err"></div>
      </div>

      <div class="col">
        <label for="pass2">Re-enter Password</label>
        <input id="pass2" name="pass2" type="password" required autocomplete="new-password">
        <div class="error" id="pass2Err"></div>
      </div>
    </div>

  </fieldset>

  <div style="display:flex;gap:12px;align-items:center">
    <button type="submit" id="submitBtn">Submit</button>
    <div id="submitResult" role="status"></div>
  </div>

</form>

<script>
/* -------------------------
   Utility & initial setup
   ------------------------- */
const pageDateEl = document.getElementById('pageDate');
const now = new Date();
pageDateEl.textContent = now.toLocaleString();

/* Populate state select. The code attempts to fetch external 'states.json' (to meet "external file" requirement)
   If that fails (e.g., running locally without that file), it falls back to an inline array.
   To provide an external file: create a states.json (array of {code,name}) and serve it next to this HTML.
*/
const statesUrl = './states.json'; // change to actual hosted path if you want a real external file
const stateSelect = document.getElementById('stateSelect');

const INLINE_STATES = [
  {code:'AL',name:'Alabama'},{code:'AK',name:'Alaska'},{code:'AZ',name:'Arizona'},{code:'AR',name:'Arkansas'},
  {code:'CA',name:'California'},{code:'CO',name:'Colorado'},{code:'CT',name:'Connecticut'},{code:'DE',name:'Delaware'},
  {code:'DC',name:'District of Columbia'},{code:'FL',name:'Florida'},{code:'GA',name:'Georgia'},{code:'HI',name:'Hawaii'},
  {code:'ID',name:'Idaho'},{code:'IL',name:'Illinois'},{code:'IN',name:'Indiana'},{code:'IA',name:'Iowa'},
  {code:'KS',name:'Kansas'},{code:'KY',name:'Kentucky'},{code:'LA',name:'Louisiana'},{code:'ME',name:'Maine'},
  {code:'MD',name:'Maryland'},{code:'MA',name:'Massachusetts'},{code:'MI',name:'Michigan'},{code:'MN',name:'Minnesota'},
  {code:'MS',name:'Mississippi'},{code:'MO',name:'Missouri'},{code:'MT',name:'Montana'},{code:'NE',name:'Nebraska'},
  {code:'NV',name:'Nevada'},{code:'NH',name:'New Hampshire'},{code:'NJ',name:'New Jersey'},{code:'NM',name:'New Mexico'},
  {code:'NY',name:'New York'},{code:'NC',name:'North Carolina'},{code:'ND',name:'North Dakota'},{code:'OH',name:'Ohio'},
  {code:'OK',name:'Oklahoma'},{code:'OR',name:'Oregon'},{code:'PA',name:'Pennsylvania'},{code:'RI',name:'Rhode Island'},
  {code:'SC',name:'South Carolina'},{code:'SD',name:'South Dakota'},{code:'TN',name:'Tennessee'},{code:'TX',name:'Texas'},
  {code:'UT',name:'Utah'},{code:'VT',name:'Vermont'},{code:'VA',name:'Virginia'},{code:'WA',name:'Washington'},
  {code:'WV',name:'West Virginia'},{code:'WI',name:'Wisconsin'},{code:'WY',name:'Wyoming'},{code:'PR',name:'Puerto Rico'}
];

function fillStateOptions(list){
  // start with blank forced option present in HTML
  for(const s of list){
    const opt = document.createElement('option');
    opt.value = s.code;
    opt.textContent = `${s.code} — ${s.name}`;
    stateSelect.appendChild(opt);
  }
}

// Try to fetch external states.json
fetch(statesUrl).then(r=>{
  if(!r.ok) throw new Error('states.json not found');
  return r.json();
}).then(data=>{
  if(Array.isArray(data) && data.length) fillStateOptions(data);
  else fillStateOptions(INLINE_STATES);
}).catch(err=>{
  // fallback
  fillStateOptions(INLINE_STATES);
});

/* -------------------------
   Dates: compute min/max
   ------------------------- */
const birthDate = document.getElementById('birthDate');
const moveInDate = document.getElementById('moveInDate');
const travelDate = document.getElementById('travelDate');

function formatDateForInput(d){
  // returns YYYY-MM-DD
  const y = d.getFullYear();
  const m = String(d.getMonth()+1).padStart(2,'0');
  const day = String(d.getDate()).padStart(2,'0');
  return `${y}-${m}-${day}`;
}

const today = new Date();
const maxBirth = today; // can't be in the future
const minBirth = new Date(today.getFullYear() - 120, today.getMonth(), today.getDate()); // 120 years ago

birthDate.min = formatDateForInput(minBirth);
birthDate.max = formatDateForInput(maxBirth);

// For move-in and travel: cannot be in the past (min = today). Allow upper horizon (max) maybe +10 years from now
moveInDate.min = formatDateForInput(today);
moveInDate.max = formatDateForInput(new Date(today.getFullYear()+10, today.getMonth(), today.getDate()));
travelDate.min = formatDateForInput(today);
travelDate.max = formatDateForInput(new Date(today.getFullYear()+10, today.getMonth(), today.getDate()));

/* -------------------------
   Salary slider (oninput)
   ------------------------- */
const salaryRange = document.getElementById('salaryRange');
const salaryValue = document.getElementById('salaryValue');

function formatCurrency(n){
  return n.toLocaleString(undefined,{style:'currency',currency:'USD',maximumFractionDigits:0});
}
salaryValue.textContent = formatCurrency(Number(salaryRange.value));
salaryRange.addEventListener('input', ()=> {
  salaryValue.textContent = formatCurrency(Number(salaryRange.value));
});

/* -------------------------
   Textarea: warn on double quotes
   ------------------------- */
const notes = document.getElementById('notes');
const notesErr = document.getElementById('notesErr');
notes.addEventListener('input', ()=>{
  if(notes.value.includes('"')){
    notesErr.textContent = 'Please avoid double quotes (") — can cause issues in databases. Consider using apostrophes (\')';
  } else {
    notesErr.textContent = '';
  }
});

/* -------------------------
   Generic helper: show validation messages
   ------------------------- */
function setError(id, msg){
  const el = document.getElementById(id);
  if(el) el.textContent = msg || '';
}

/* -------------------------
   Specific field validations (live/oninput)
   ------------------------- */
const form = document.getElementById('mainForm');

const validators = {
  firstName: (el)=>{
    if(!el.value) return 'First name is required';
    if(!/^[A-Za-z'\-]{1,30}$/.test(el.value)) return 'Only letters, apostrophes, dashes allowed (1–30 chars)';
    return '';
  },
  middleInitial: (el)=>{
    if(!el.value) return '';
    if(!/^[A-Za-z]$/.test(el.value)) return 'Middle initial must be a single letter';
    return '';
  },
  lastName: (el)=>{
    if(!el.value) return 'Last name is required';
    if(!/^[A-Za-z'\-2-5]{1,30}$/.test(el.value)) return 'Only letters, apostrophes, dashes and digits 2–5 allowed (1–30 chars)';
    return '';
  },
  birthDate: (el)=>{
    if(!el.value) return 'Birthdate is required';
    const d = new Date(el.value);
    if(isNaN(d)) return 'Invalid date format';
    if(d > today) return 'Birthdate cannot be in the future';
    const diffYears = today.getFullYear() - d.getFullYear() - ((today.getMonth()<d.getMonth() || (today.getMonth()===d.getMonth() && today.getDate()<d.getDate()))?1:0);
    if(diffYears > 120) return 'Birthdate cannot be more than 120 years ago';
    return '';
  },
  moveInDate: (el)=>{
    if(!el.value) return 'Move-in date is required';
    const d = new Date(el.value);
    if(isNaN(d)) return 'Invalid date';
    if(d < new Date(formatDateForInput(today))) return 'Move-in date cannot be in the past';
    return '';
  },
  travelDate: (el)=>{
    if(!el.value) return 'Travel date is required';
    const d = new Date(el.value);
    if(isNaN(d)) return 'Invalid date';
    if(d < new Date(formatDateForInput(today))) return 'Travel date cannot be in the past';
    return '';
  },
  ssn: (el)=>{
    if(!el.value) return '';
    if(!/^[0-9]{3}-[0-9]{2}-[0-9]{4}$/.test(el.value)) return 'SSN must be in 123-45-6789 format or left blank';
    return '';
  },
  idNumber: (el)=>{
    if(!el.value) return 'ID number is required';
    // No other checks — it's obscured. But ensure length
    if(el.value.length < 3) return 'ID seems too short';
    return '';
  },
  email: (el)=>{
    if(!el.value) return 'Email required';
    if(!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(el.value)) return 'Invalid email format';
    return '';
  },
  phone: (el)=>{
    if(!el.value) return 'Phone is required';
    if(!/^[0-9]{3}-[0-9]{3}-[0-9]{4}$/.test(el.value)) return 'Phone must be in 000-000-0000 format';
    return '';
  },
  addr1: (el)=>{
    if(!el.value) return 'Address Line 1 required';
    if(el.value.length<2 || el.value.length>30) return 'Address must be 2–30 characters';
    return '';
  },
  addr2: (el)=>{
    if(!el.value) return '';
    if(el.value.length<2 || el.value.length>30) return 'Address Line 2 must be 2–30 characters if provided';
    return '';
  },
  city: (el)=>{
    if(!el.value) return 'City required';
    if(el.value.length<2 || el.value.length>30) return 'City must be 2–30 characters';
    return '';
  },
  stateSelect: (el)=>{
    if(!el.value) return 'Please select a state';
    return '';
  },
  zip: (el)=>{
    if(!el.value) return 'ZIP required';
    if(!/^[0-9]{5}(-[0-9]{4})?$/.test(el.value)) return 'ZIP must be 5 digits or ZIP+4 (e.g., 77002 or 77002-1234)';
    return '';
  },
  housing: (/*not element*/) =>{
    const checked = form.querySelector('input[name="housing"]:checked');
    if(!checked) return 'Please choose housing status';
    return '';
  },
  vaccinated: ()=>{
    const checked = form.querySelector('input[name="vaccinated"]:checked');
    if(!checked) return 'Please indicate vaccination status';
    return '';
  },
  userId: (el)=>{
    if(!el.value) return 'User ID required';
    if(!/^(?!\d)[A-Za-z0-9_-]{5,30}$/.test(el.value)) return '5–30 chars; first char cannot be a number; only letters, numbers, underscore or dash; no spaces';
    return '';
  },
  pass1: (el)=>{
    const v = el.value || '';
    if(v.length < 8) return 'Password must be at least 8 characters';
    if(v.length > 30) return 'Password must be at most 30 characters';
    if(v.includes('"')) return 'Double quotes (") are not allowed in passwords';
    if(!/[A-Z]/.test(v)) return 'Password must contain at least one uppercase letter';
    if(!/[a-z]/.test(v)) return 'Password must contain at least one lowercase letter';
    if(!/[0-9]/.test(v)) return 'Password must contain at least one digit';
    // at least one special (non alphanumeric). Disallow quote handled above.
    if(!/[^A-Za-z0-9]/.test(v)) return 'Password must contain at least one special character (e.g. !@#$%)';
    // ensure not equal to userId or contain user id part
    const uid = document.getElementById('userId').value || '';
    if(uid && v.toLowerCase().includes(uid.toLowerCase())) return 'Password cannot contain the User ID';
    return '';
  },
  pass2: (el)=>{
    const v = el.value || '';
    const v1 = document.getElementById('pass1').value || '';
    if(v !== v1) return 'Passwords do not match';
    return '';
  }
};

// Attach live validation for fields with IDs in validators
Object.keys(validators).forEach(key=>{
  const el = document.getElementById(key);
  if(el){
    el.addEventListener('input', ()=> {
      const msg = validators[key](el);
      setError(key + 'Err', msg);
    });
    el.addEventListener('blur', ()=> {
      const msg = validators[key](el);
      setError(key + 'Err', msg);
    });
  }
});

// For radio-group validators (housing, vaccinated) show on change
['housing','vaccinated'].forEach(name=>{
  const els = form.querySelectorAll(`input[name="${name}"]`);
  els.forEach(e => e.addEventListener('change', ()=> {
    const msg = validators[name]();
    setError(name + 'Err', msg);
  }));
});

/* -------------------------
   Submit handling
   ------------------------- */

form.addEventListener('submit', (ev)=>{
  ev.preventDefault();
  // Clear previous submit result
  const submitResult = document.getElementById('submitResult');
  submitResult.textContent = '';

  // Validate all fields
  let hasErr = false;
  // Run through validator entries
  for(const key in validators){
    let el = document.getElementById(key);
    let msg;
    if(el) msg = validators[key](el);
    else msg = validators[key](); // radio groups
    setError(key + 'Err', msg);
    if(msg) hasErr = true;
  }

  // Additional check: notes double-quote
  if(notes.value.includes('"')) {
    setError('notesErr','Notes contains double quotes ("). Please remove.');
    hasErr = true;
  }

  if(hasErr){
    submitResult.className = 'msg err';
    submitResult.textContent = 'Form has errors — please fix the messages shown near each field.';
    return;
  }

  // On successful validation: normalize and show processed data (simulated)
  // Normalize userId -> lowercase
  const userIdEl = document.getElementById('userId');
  const normalizedUserId = userIdEl.value.toLowerCase();
  userIdEl.value = normalizedUserId;

  // Truncate ZIP to first 5 digits if ZIP+4 provided, and redisplay truncated version
  const zipEl = document.getElementById('zip');
  const zipVal = zipEl.value;
  const truncatedZip = zipVal.match(/^([0-9]{5})/)? zipVal.match(/^([0-9]{5})/)[1] : zipVal;
  zipEl.value = truncatedZip;

  // Prepare a small result summary (we won't display SSN or passwords)
  const result = {
    firstName: document.getElementById('firstName').value,
    middleInitial: document.getElementById('middleInitial').value,
    lastName: document.getElementById('lastName').value,
    birthDate: document.getElementById('birthDate').value,
    moveInDate: document.getElementById('moveInDate').value,
    travelDate: document.getElementById('travelDate').value,
    email: document.getElementById('email').value,
    phone: document.getElementById('phone').value,
    address: {
      addr1: document.getElementById('addr1').value,
      addr2: document.getElementById('addr2').value,
      city: document.getElementById('city').value,
      state: document.getElementById('stateSelect').value,
      zip: document.getElementById('zip').value
    },
    salaryDesired: document.getElementById('salaryRange').value,
    userId: document.getElementById('userId').value
  };

  submitResult.className = 'msg ok';
  submitResult.textContent = 'Form validated successfully — preview of saved fields shown in console (sensitive fields are NOT shown).';

  // For demo purposes, log non-sensitive preview to console
  console.log('=== Form submission preview (sensitive fields hidden) ===');
  console.log(result);
  console.log('Sensitive fields (not logged): SSN, ID number, password fields.');

  // Here: you would send the form data to your server via fetch/AJAX
  // e.g., fetch('/submit', {method:'POST', body: formData})
});

/* -------------------------
   Small UX improvements: show immediate error for pattern-mismatching typed content on blur
   ------------------------- */
['firstName','lastName','email','phone','zip','userId'].forEach(id=>{
  const el=document.getElementById(id);
  if(!el) return;
  el.addEventListener('blur', ()=>{
    const msg = validators[id] ? validators[id](el) : '';
    setError(id + 'Err', msg);
  });
});

/* -------------------------
   Accessibility: keyboard focus visible etc (light)
   ------------------------- */
document.addEventListener('keydown', (e)=>{
  // nothing special yet
});
</script>

</body>
</html>
