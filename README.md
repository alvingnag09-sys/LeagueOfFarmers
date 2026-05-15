<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LEAGUE OF FARMERS</title>
<style>
  :root{
    --bg:#0f1117;
    --card:#1e1f26;
    --card2:#2d2f39;
    --text:#ececec;
    --muted:#9aa0a6;
    --green:#10a37f;
    --green-dark:#0d8266;
    --border:#2a2d36;
  }
  *{margin:0;padding:0;box-sizing:border-box;font-family:system-ui,-apple-system,Segoe UI,Roboto,Arial}
  body{background:var(--bg);color:var(--text);min-height:100vh}

  /* Auth Page */
 .auth-container{display:flex;align-items:center;justify-content:center;min-height:100vh;padding:20px}
 .auth-box{background:var(--card);padding:32px;border-radius:16px;width:100%;max-width:420px;border:1px solid var(--border)}
 .auth-box h1{text-align:center;margin-bottom:8px;font-size:28px}
 .auth-box p{text-align:center;color:var(--muted);margin-bottom:24px}
 .input-group{margin-bottom:16px}
 .input-group label{display:block;margin-bottom:6px;font-size:14px;color:var(--muted)}
 .input-group input{width:100%;padding:12px;border-radius:8px;border:1px solid var(--border);background:var(--bg);color:var(--text);outline:none}
 .password-wrap{position:relative}
 .password-wrap button{position:absolute;right:10px;top:50%;transform:translateY(-50%);background:none;border:none;color:var(--muted);cursor:pointer;font-size:14px}
 .btn{width:100%;padding:12px;border:none;border-radius:8px;background:var(--green);color:white;font-weight:600;cursor:pointer;margin-top:8px}
 .btn:hover{background:var(--green-dark)}
 .btn-secondary{background:transparent;border:1px solid var(--border)}
 .toggle-link{text-align:center;margin-top:16px;color:var(--muted);font-size:14px}
 .toggle-link a{color:var(--green);cursor:pointer;text-decoration:none}
 .error{color:#ff6b6b;font-size:13px;margin-top:6px;display:none}

  /* App Layout */
 .app{display:none;flex-direction:column;height:100vh}
  header{background:var(--card);border-bottom:1px solid var(--border);padding:12px 16px;display:flex;align-items:center;justify-content:space-between}
  header h2{font-size:18px}
 .hamburger{display:none;background:none;border:none;color:var(--text);font-size:24px;cursor:pointer}

  nav{display:flex;background:var(--card);border-bottom:1px solid var(--border);overflow-x:auto}
  nav button{flex:0 0 auto;padding:14px 20px;background:none;border:none;color:var(--muted);cursor:pointer;font-weight:500;white-space:nowrap}
  nav button.active{color:var(--green);border-bottom:2px solid var(--green)}

  main{flex:1;overflow-y:auto;padding:16px}

  /* Stories Scroller like Facebook */
 .stories{display:flex;gap:12px;overflow-x:auto;padding-bottom:8px;margin-bottom:16px}
 .stories::-webkit-scrollbar{display:none}
 .story{flex:0 0 80px;text-align:center}
 .story-avatar{width:70px;height:70px;border-radius:50%;border:3px solid var(--green);padding:2px;margin-bottom:4px}
 .story img{width:100%;height:100%;border-radius:50%;object-fit:cover}
 .story p{font-size:12px;color:var(--muted);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}

 .post{background:var(--card);border-radius:12px;padding:16px;margin-bottom:16px;border:1px solid var(--border)}
 .post h3{margin-bottom:8px}
 .post p{color:var(--muted)}

  /* Responsive */
  @media(max-width:768px){
   .hamburger{display:block}
    nav{display:none;flex-direction:column;position:absolute;top:60px;left:0;right:0;z-index:100}
    nav.show{display:flex}
  }
</style>
</head>
<body>

<!-- AUTH PAGE -->
<div class="auth-container" id="authPage">
  <div class="auth-box">
    <h1>LEAGUE OF FARMERS</h1>
    <p id="authSubtitle">Login to continue</p>

    <div id="loginForm">
      <div class="input-group">
        <label>Username</label>
        <input type="text" id="loginUsername" placeholder="Enter username">
      </div>
      <div class="input-group">
        <label>Password</label>
        <div class="password-wrap">
          <input type="password" id="loginPassword" placeholder="Enter password">
          <button type="button" onclick="togglePass('loginPassword',this)">Show</button>
        </div>
        <div class="error" id="loginError">Invalid username or password</div>
      </div>
      <button class="btn" onclick="login()">Login</button>
      <div class="toggle-link">Don't have an account? <a onclick="showSignup()">Sign up</a></div>
    </div>

    <div id="signupForm" style="display:none">
      <div class="input-group">
        <label>Full Name</label>
        <input type="text" id="signupName" placeholder="Juan Dela Cruz">
      </div>
      <div class="input-group">
        <label>First Name</label>
        <input type="text" id="signupFirst" placeholder="Juan">
      </div>
      <div class="input-group">
        <label>Middle Name</label>
        <input type="text" id="signupMiddle" placeholder="Santos">
      </div>
      <div class="input-group">
        <label>Username</label>
        <input type="text" id="signupUsername" placeholder="Choose a username">
        <div class="error" id="signupError">Username already taken</div>
      </div>
      <div class="input-group">
        <label>Password</label>
        <div class="password-wrap">
          <input type="password" id="signupPassword" placeholder="Create password">
          <button type="button" onclick="togglePass('signupPassword',this)">Show</button>
        </div>
      </div>
      <button class="btn" onclick="signup()">Sign Up</button>
      <div class="toggle-link">Already have an account? <a onclick="showLogin()">Login</a></div>
    </div>
  </div>
</div>

<!-- MAIN APP -->
<div class="app" id="appPage">
  <header>
    <h2>LEAGUE OF FARMERS</h2>
    <button class="hamburger" onclick="toggleMenu()">☰</button>
  </header>

  <nav id="navMenu">
    <button class="active" onclick="switchTab('home',this)">Home</button>
    <button onclick="switchTab('farm',this)">Farm</button>
    <button onclick="switchTab('message',this)">Message</button>
    <button onclick="switchTab('friends',this)">Friends</button>
    <button onclick="switchTab('marketplace',this)">Marketplace</button>
    <button onclick="switchTab('profile',this)">Profile</button>
    <button onclick="logout()">Logout</button>
  </nav>

  <main id="mainContent">
    <!-- Content loads here -->
  </main>
</div>

<script>
const authPage = document.getElementById('authPage');
const appPage = document.getElementById('appPage');
const mainContent = document.getElementById('mainContent');

// Check if logged in
if(localStorage.getItem('lof_currentUser')){
  showApp();
}

// Toggle password visibility
function togglePass(id,btn){
  const input = document.getElementById(id);
  if(input.type === 'password'){
    input.type = 'text';
    btn.textContent = 'Hide';
  }else{
    input.type = 'password';
    btn.textContent = 'Show';
  }
}

function showSignup(){
  document.getElementById('loginForm').style.display='none';
  document.getElementById('signupForm').style.display='block';
  document.getElementById('authSubtitle').textContent='Create your account';
}

function showLogin(){
  document.getElementById('signupForm').style.display='none';
  document.getElementById('loginForm').style.display='block';
  document.getElementById('authSubtitle').textContent='Login to continue';
}

function signup(){
  const name = document.getElementById('signupName').value.trim();
  const first = document.getElementById('signupFirst').value.trim();
  const middle = document.getElementById('signupMiddle').value.trim();
  const username = document.getElementById('signupUsername').value.trim();
  const password = document.getElementById('signupPassword').value.trim();
  const error = document.getElementById('signupError');

  if(!name||!first||!username||!password){
    alert('Please fill all required fields');
    return;
  }

  let users = JSON.parse(localStorage.getItem('lof_users')||'{}');
  if(users[username]){
    error.style.display='block';
    return;
  }

  users[username]={name,first,middle,username,password};
  localStorage.setItem('lof_users',JSON.stringify(users));
  localStorage.setItem('lof_currentUser',username);
  showApp();
}

function login(){
  const username = document.getElementById('loginUsername').value.trim();
  const password = document.getElementById('loginPassword').value.trim();
  const error = document.getElementById('loginError');

  let users = JSON.parse(localStorage.getItem('lof_users')||'{}');
  if(users[username] && users[username].password===password){
    localStorage.setItem('lof_currentUser',username);
    showApp();
  }else{
    error.style.display='block';
  }
}

function logout(){
  localStorage.removeItem('lof_currentUser');
  location.reload();
}

function showApp(){
  authPage.style.display='none';
  appPage.style.display='flex';
  switchTab('home',document.querySelector('nav button'));
}

function toggleMenu(){
  document.getElementById('navMenu').classList.toggle('show');
}

function switchTab(tab,btn){
  document.querySelectorAll('nav button').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  document.getElementById('navMenu').classList.remove('show');

  const user = localStorage.getItem('lof_currentUser');
  const users = JSON.parse(localStorage.getItem('lof_users')||'{}');
  const name = users[user]?.first || user;

  let html='';
  if(tab==='home'){
    html=`
      <div class="stories">
        <div class="story">
          <div class="story-avatar"><img src="https://i.pravatar.cc/100?u=${user}"></div>
          <p>Your Story</p>
        </div>
        <div class="story"><div class="story-avatar"><img src="https://i.pravatar.cc/100?u=1"></div><p>FarmerJoe</p></div>
        <div class="story"><div class="story-avatar"><img src="https://i.pravatar.cc/100?u=2"></div><p>CropQueen</p></div>
        <div class="story"><div class="story-avatar"><img src="https://i.pravatar.cc/100?u=3"></div><p>HarvestKing</p></div>
        <div class="story"><div class="story-avatar"><img src="https://i.pravatar.cc/100?u=4"></div><p>LandLord</p></div>
      </div>
      <div class="post"><h3>Welcome ${name}!</h3><p>This is your home feed. Scroll to see farm updates from your friends.</p></div>
      <div class="post"><h3>Farm Tip</h3><p>Water your crops early morning for better yield. Post your harvest!</p></div>
      <div class="post"><h3>Market Update</h3><p>Corn prices are up 12% this week. Check Marketplace for deals.</p></div>
    `;
  }else if(tab==='farm'){
    html=`<div class="post"><h3>Your Farm</h3><p>Farm management coming soon. Plant, grow, harvest!</p></div>`;
  }else if(tab==='profile'){
    html=`<div class="post"><h3>Profile</h3><p>Name: ${users[user]?.name}<br>Username: ${user}</p></div>`;
  }else{
    html=`<div class="post"><h3>${tab.charAt(0).toUpperCase()+tab.slice(1)}</h3><p>This section is under construction.</p></div>`;
  }
  mainContent.innerHTML=html;
}
</script>
</body>
</html>
