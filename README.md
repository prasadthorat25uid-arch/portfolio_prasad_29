<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Prasad Sudhir Thorat — Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700;800&family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
  :root{
    --bg-void:#080B10;
    --bg-panel:#10161F;
    --bg-panel-2:#141C27;
    --border:#1F2C3B;
    --border-soft:#182230;
    --teal:#45E0C4;
    --teal-dim:#2A8F7D;
    --amber:#F5A623;
    --text-1:#E7EEF5;
    --text-2:#8FA1B3;
    --text-3:#546477;
    --mono:'JetBrains Mono', monospace;
    --sans:'Inter', sans-serif;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--bg-void);
    color:var(--text-1);
    font-family:var(--sans);
    line-height:1.6;
    overflow-x:hidden;
  }
  body::before{
    content:'';
    position:fixed;inset:0;
    background-image:
      linear-gradient(var(--border-soft) 1px, transparent 1px),
      linear-gradient(90deg, var(--border-soft) 1px, transparent 1px);
    background-size:48px 48px;
    opacity:0.35;
    z-index:0;
    pointer-events:none;
    mask-image:radial-gradient(ellipse 80% 60% at 50% 0%, black 30%, transparent 75%);
  }
  .wrap{position:relative;z-index:1;}
  a{color:inherit;text-decoration:none;}
  ::selection{background:var(--teal);color:#04120F;}

  /* ---------- NAV ---------- */
  nav{
    position:fixed;top:0;left:0;right:0;z-index:50;
    display:flex;align-items:center;justify-content:space-between;
    padding:18px 5vw;
    background:rgba(8,11,16,0.82);
    backdrop-filter:blur(10px);
    border-bottom:1px solid var(--border-soft);
  }
  .nav-id{
    font-family:var(--mono);font-size:13px;color:var(--teal);
    display:flex;align-items:center;gap:8px;
  }
  .nav-id .dot{width:7px;height:7px;border-radius:50%;background:var(--teal);box-shadow:0 0 8px var(--teal);animation:pulse 2s infinite;}
  @keyframes pulse{0%,100%{opacity:1;}50%{opacity:0.3;}}
  .nav-links{display:flex;gap:32px;font-family:var(--mono);font-size:12.5px;letter-spacing:0.03em;}
  .nav-links a{color:var(--text-2);position:relative;padding:4px 0;transition:color .2s;}
  .nav-links a:hover{color:var(--teal);}
  .nav-links a::before{content:'';}
  @media(max-width:820px){.nav-links{display:none;}}

  /* ---------- HERO / BOOT SEQUENCE ---------- */
  .hero{
    min-height:100vh;
    display:flex;flex-direction:column;justify-content:center;
    padding:120px 5vw 80px;
    position:relative;
  }
  .terminal{
    max-width:640px;
    font-family:var(--mono);
    font-size:14px;
    color:var(--teal);
    min-height:190px;
  }
  .terminal .line{opacity:0;white-space:pre;overflow:hidden;}
  .terminal .prompt{color:var(--text-3);}
  .terminal .ok{color:var(--teal);}
  .terminal .granted{color:var(--amber);font-weight:700;}
  .cursor{display:inline-block;width:8px;height:15px;background:var(--teal);vertical-align:middle;animation:blink 1s step-end infinite;margin-left:2px;}
  @keyframes blink{50%{opacity:0;}}

  .profile-reveal{
    opacity:0;transform:translateY(18px);
    transition:opacity .7s ease, transform .7s ease;
    margin-top:40px;
    display:flex;align-items:center;gap:44px;
    flex-wrap:wrap;
  }
  .profile-reveal.show{opacity:1;transform:translateY(0);}
  .photo-frame{
    position:relative;width:180px;height:180px;flex-shrink:0;
  }
  .photo-frame img{
    width:100%;height:100%;object-fit:cover;object-position:top center;
    border-radius:8px;
    border:1px solid var(--border);
    filter:grayscale(15%) contrast(1.05);
  }
  .photo-frame::before{
    content:'';position:absolute;inset:-8px;
    border:1px solid var(--teal-dim);border-radius:12px;
    opacity:0.5;
  }
  .photo-frame::after{
    content:'● LIVE';
    position:absolute;bottom:-14px;left:50%;transform:translateX(-50%);
    font-family:var(--mono);font-size:9.5px;letter-spacing:.12em;
    color:var(--amber);background:var(--bg-void);
    padding:2px 8px;border:1px solid var(--border);border-radius:20px;
  }
  .id-block h1{
    font-family:var(--mono);
    font-size:clamp(28px,4vw,46px);
    font-weight:700;
    letter-spacing:-0.01em;
    color:var(--text-1);
  }
  .id-block .role{
    color:var(--teal);font-family:var(--mono);font-size:14px;margin-top:8px;
    letter-spacing:.02em;
  }
  .id-block .meta{
    color:var(--text-2);font-size:13.5px;margin-top:6px;
  }
  .id-block .tagline{
    margin-top:18px;max-width:480px;color:var(--text-2);font-size:15px;
  }
  .cta-row{margin-top:26px;display:flex;gap:14px;flex-wrap:wrap;align-items:center;}
  .btn{
    font-family:var(--mono);font-size:12.5px;letter-spacing:.03em;
    padding:11px 20px;border-radius:6px;
    display:inline-flex;align-items:center;gap:8px;
    transition:all .2s ease;
    border:1px solid var(--border);
  }
  .btn-primary{background:var(--teal);color:#04120F;font-weight:700;border-color:var(--teal);}
  .btn-primary:hover{background:#5FF0D6;transform:translateY(-1px);}
  .btn-ghost{color:var(--text-1);}
  .btn-ghost:hover{border-color:var(--teal-dim);color:var(--teal);}
  .icon-row{display:flex;gap:10px;}
  .icon-btn{
    width:38px;height:38px;border-radius:6px;border:1px solid var(--border);
    display:flex;align-items:center;justify-content:center;
    color:var(--text-2);transition:all .2s ease;
  }
  .icon-btn:hover{border-color:var(--teal);color:var(--teal);transform:translateY(-2px);}
  .icon-btn svg{width:17px;height:17px;}

  /* ---------- SECTION SHELL ---------- */
  section{padding:100px 5vw;position:relative;border-top:1px solid var(--border-soft);}
  .eyebrow{
    font-family:var(--mono);font-size:12px;color:var(--amber);
    letter-spacing:.15em;text-transform:uppercase;margin-bottom:14px;
    display:flex;align-items:center;gap:10px;
  }
  .eyebrow::before{content:'//';color:var(--text-3);}
  h2.sec-title{
    font-family:var(--mono);font-size:clamp(24px,3vw,34px);font-weight:700;
    margin-bottom:48px;color:var(--text-1);
  }
  .section-inner{max-width:1180px;margin:0 auto;}

  /* ---------- ABOUT ---------- */
  .about-grid{display:grid;grid-template-columns:1.3fr 1fr;gap:60px;align-items:start;}
  .about-grid p{color:var(--text-2);font-size:16px;margin-bottom:18px;max-width:60ch;}
  .about-grid p strong{color:var(--text-1);font-weight:600;}
  .fact-panel{
    background:var(--bg-panel);border:1px solid var(--border);border-radius:10px;
    padding:24px 26px;
  }
  .fact-row{display:flex;justify-content:space-between;padding:12px 0;border-bottom:1px solid var(--border-soft);font-size:13.5px;}
  .fact-row:last-child{border-bottom:none;}
  .fact-row span:first-child{color:var(--text-3);font-family:var(--mono);}
  .fact-row span:last-child{color:var(--text-1);text-align:right;}

  /* ---------- SKILLS ---------- */
  .skills-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:20px;}
  .skill-card{
    background:var(--bg-panel);border:1px solid var(--border);border-radius:10px;padding:22px 24px;
  }
  .skill-card .cat{font-family:var(--mono);font-size:12px;color:var(--amber);letter-spacing:.08em;text-transform:uppercase;margin-bottom:14px;}
  .skill-tags{display:flex;flex-wrap:wrap;gap:8px;}
  .skill-tag{
    font-family:var(--mono);font-size:12px;color:var(--text-2);
    border:1px solid var(--border);padding:6px 11px;border-radius:20px;
    transition:all .2s ease;
  }
  .skill-tag:hover{border-color:var(--teal);color:var(--teal);}

  /* ---------- EXPERIENCE ---------- */
  .exp-card{
    background:var(--bg-panel);border:1px solid var(--border);border-radius:10px;
    padding:30px 32px;position:relative;overflow:hidden;
  }
  .exp-card::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:var(--teal);}
  .exp-head{display:flex;justify-content:space-between;flex-wrap:wrap;gap:10px;margin-bottom:16px;}
  .exp-head h3{font-size:19px;color:var(--text-1);}
  .exp-head .company{color:var(--teal);font-size:14px;margin-top:4px;}
  .exp-head .date{font-family:var(--mono);font-size:12px;color:var(--text-3);border:1px solid var(--border);padding:5px 12px;border-radius:20px;height:fit-content;}
  .exp-card ul{list-style:none;color:var(--text-2);font-size:14.5px;}
  .exp-card li{padding-left:20px;position:relative;margin-bottom:9px;}
  .exp-card li::before{content:'▹';position:absolute;left:0;color:var(--teal);}

  /* ---------- CERTIFICATIONS ---------- */
  .cert-groups{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:22px;}
  .cert-group{
    background:var(--bg-panel);border:1px solid var(--border);border-radius:10px;
    padding:24px 26px;
  }
  .cert-group-head{display:flex;align-items:center;gap:10px;margin-bottom:16px;padding-bottom:14px;border-bottom:1px solid var(--border-soft);}
  .cert-group-head .icon{
    width:32px;height:32px;border-radius:7px;background:var(--bg-panel-2);
    display:flex;align-items:center;justify-content:center;color:var(--teal);
    border:1px solid var(--border);
  }
  .cert-group-head h3{font-size:14.5px;color:var(--text-1);font-family:var(--mono);letter-spacing:.02em;}
  .cert-list{list-style:none;}
  .cert-item{
    display:flex;justify-content:space-between;gap:12px;
    padding:9px 0;font-size:13.5px;color:var(--text-2);border-bottom:1px dashed var(--border-soft);
  }
  .cert-item:last-child{border-bottom:none;}
  .cert-item .name{color:var(--text-1);}
  .cert-item .issuer{color:var(--text-3);font-family:var(--mono);font-size:11.5px;white-space:nowrap;text-align:right;}

  /* ---------- TIMELINE (Achievements) ---------- */
  .timeline{position:relative;padding-left:28px;}
  .timeline::before{content:'';position:absolute;left:5px;top:6px;bottom:6px;width:1px;background:var(--border);}
  .t-item{position:relative;padding-bottom:34px;}
  .t-item:last-child{padding-bottom:0;}
  .t-item::before{
    content:'';position:absolute;left:-28px;top:4px;width:11px;height:11px;border-radius:50%;
    background:var(--bg-void);border:2px solid var(--teal);
  }
  .t-item .t-date{font-family:var(--mono);font-size:11.5px;color:var(--amber);letter-spacing:.05em;}
  .t-item h4{font-size:16px;color:var(--text-1);margin:6px 0 4px;}
  .t-item p{color:var(--text-2);font-size:13.5px;}

  /* ---------- CONTACT / FOOTER ---------- */
  .contact-panel{
    background:var(--bg-panel);border:1px solid var(--border);border-radius:14px;
    padding:56px 5vw;text-align:center;
    position:relative;overflow:hidden;
  }
  .contact-panel h2{font-family:var(--mono);font-size:clamp(22px,3vw,32px);margin-bottom:14px;}
  .contact-panel p{color:var(--text-2);max-width:480px;margin:0 auto 30px;}
  footer{padding:34px 5vw;text-align:center;font-family:var(--mono);font-size:11.5px;color:var(--text-3);border-top:1px solid var(--border-soft);}

  @media(max-width:720px){
    .about-grid{grid-template-columns:1fr;}
    section{padding:70px 6vw;}
  }
</style>
</head>
<body>

<div class="wrap">

  <nav>
    <div class="nav-id"><span class="dot"></span> prasad@sanjivani:~$</div>
    <div class="nav-links">
      <a href="#about">about</a>
      <a href="#skills">skills</a>
      <a href="#experience">experience</a>
      <a href="#certifications">certifications</a>
      <a href="#achievements">achievements</a>
      <a href="#contact">contact</a>
    </div>
  </nav>

  <!-- HERO -->
  <header class="hero">
    <div class="terminal" id="terminal"></div>
    <div class="profile-reveal" id="profileReveal">
      <div class="photo-frame">
        <img src="data:image/jpeg;base64,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IkRaAtWyZOl5rp8dfV1drUx08MZ0AAAAAAAAAAAAAAB6vpaO9rNOX6blbPIrMaxkvjyXMVvSyIJYTVZrMFItSayTEotWS0SsiREwJgLImphBKJETARIraClMuPOskxNkkJOG9Vm0SREwRMCVSzERExBRMRJUJETaUrWYWtMlJZJGTHKZ76+TWclq21mCEsrJZWRMSIYZdzreT67HXe09zRzrxhnQAAAAAAAAAAAAAAHubeDPrOHlOq5TWfKraLm+TFlua1vSoQhCVrW1RTJjmskwSZgWFkolJgAJmtqJhIIWUSQCYCKXpLeYlCIWlosJgImomJKL1WqUVWsUm0BIhKxEitbUlnHlpLExKgTMEyZNe1mzOG+s2ksIJZELWszLu9bynWY6behv+dnXkjOgAAAAAAAAAAAAAAOjyGs4eT6zktZ8sXLNhzXNcd6EILJJGPJSW2LJjMhIJJIsma2AImJFq2sRMICgIkQCKWrLeYlGLJRZmYBBMBCYBCxMTEk2QCYtBAJIK1TNIkY7VvLWJgAkgvbFKbF9bLrOaIm5AiLY5fT6vl+rx1z+b6XmS+WM6AAAAAAAAAAAAAATFzpBvOtyfT8lc6Y1iMuPKUpeqVCygITLWlqy5JibAJRNi1ZJgJRKLUsWgqsgi1QBEwVhMszApelpbVLJiYAETAiYWEoSWImCyJISIrNJYmt1mJJjTEskkJETa9Yq54TDN6y5Mute5zWrGpbDekvt9Ty/T465/L9TyY84Z0AAAAAAAAAAAAAAz4Ns9wbz5HKdHzFzE1trC9LFaqgSyCtoFIWltMTYBKJRNbUJImBNqXSJKgBNQSREwUtSc2+OYW0oslAmAAQLCRWSExNIkJiUhMFaWrNLRJMSSsTCzMWIRKWtWbJmLWIkUrkSzChaIS+r1PFdRnfted6OvL4AzoAAAAAAAAAAAAABvaPpHqjeed5rp+cucVqWubprc4w1AiYmBjvRV6XiZibBJElRaJQCYBelklCgAImBAMc1Z1XLjyExKyAARIIkQFQCYEoC1LitqlCYJglEkY8mOVkpNJiUtNZqclMliLQiGKWawmpLRk6TwPfXo0TNcwzYcaAAAAAA/8QAAv/aAAwDAQACAAMAAAAh999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999999976+/wBfffffffffffffffffffffffffffffffffffffffffffffffffffffffff6kYAAAAEsuvfffffffffffffffffffffffffffffffffffffffffffffffffffeQhCstWKLrigF/ffffffffffffffffffffffffffffffffffffffffffffffffe4At4qRHBCWcimwM/fffffffffffffffffffffffffffffffffffffffffffffffaQKgpucybGToshhCk/fffffffffffffffffffffffffffffffffffffffffffffaAPrii2YBFurjpvhhwtfffffffffffffffffffffffffffffffffffffffffffffaxvvguiMBSoivsossgPPfffffffffffffffffffffffffffffffffffffffffffaxGivnisydi80wplgvot/fffffffffffffffffffffffffffffffffffffffffffaVPTplqqHIIiCHTx4vqlvfffffffffffffffffffffffffffffffffffffffffffaxpVks6DWF3hqwSQIo6hvfffffffffffffffffffffffffffffffffffffffffffa1xjoYHKTtm2UhBsy/Yz/fffffffffffffffffffffffffffffffffffffffffffawCGPy1SRsoqMJ1BIuwv8A33333333333333333333333333333333333333333332oRihfvQzWKEfZgPTR9b333333333333333333333333333333333333333333332oeS0n/6Uiu+wF6w8Y9H333333333333333333333333333333333333333333332oW5ppQmwpXoKzXX6G4D333333333333333333333333333333333333333333330pMRxNy0F4OsEq12VNNf333333333333333333333333333333333333333333332sQ+RQtR6dAd1pdlq4PX3333333333333333333333333333333333333333333338rMMlt1JAlcWsEu1MnT3333333333333333333333333333333333333333333330oRa4zHqPgqsU7/w4J/33333333333333333333333333333333333333333333334Btuw0+WpbiE/i0pT333333333333333333333333333333333333333333333330AG2i7NFUvz3VbUDX333333333333333333333333333333333333333333333333wD+zOVXbUyZgK0vz3333333333333333333333333333333333333333333333330tPwUm7A5Xz6zoP/3333333333333333333333333333333333333333333333330FR7DVMTW6BxxWrb333333333333333333333333333333333333333333333333sKKl1iJnLtHsY2IP8A99999999999999999999999999999999999999999999995pDSf37m5CqgKHoSLx899999999999999999999999999999999999999999999/oGbyb/ACuaEB3pfZ6DBAAgvvfffffffffffffffffffffffffffffffffffffff44g86rJzAzLZTW/UO5X6OqgAM88/fffffffffffffffffffffffffffffffffeewgmy0/ItD59De4rDAP6tq5f9ALjQAdd/ffffffffffffffffffffffffffffecYhGswA9mAnPaUw81Bv9COy4dNNKMkWriEkP/fffffffffffffffffffffffffaIwDKMGzUJr5o4YLMAFAMqwO3KOTdcBOORmGSQtvfffffffffffffffffffffffcYEdWJzmCetw9udKightJeV/KLM7YQ0datMDazzkfffffffffffffffffffffffaQApIS+7k4XYVjMS50g3p5n5/ZYUjZYSVaeTf6Q+wH/AH33333333333333333333sIfw6vvet7V2MfHGRvoJdXa+zlXGS2HHXW2x3VGKwhT333333333333333333332sU0lFP2aa+GlRQ+LNLAJcBM7j33ElXV3HD5c/BI9QlL333333333333333333330AITSxffNTwmXxFCVfiYJIU/T5+3mh3ECXBK8OpRqeYX333333333333333333330MNgcdrYPACdo5l2njL0IIG2Maqg4hTDHmCapZJU+KJL333333333333333333330AtxLM8TngAIX11hES6iIYC2EdZrerZIjVZdau72wSgr73333333333333333332oBFdjiCiCxw7fIbC1m9IsqjmX5LYrI40HKeu+17cwpeDP3333333333333333332kD8ClGTnjSAuLJBZOQUyp8G91nZrZlR81DRwZ8/E5h2ND3333333333333333333sTQbKXRSDjRsKLWKqLldeginTQCw29nPjiyU6BugGMj0L3333333333333333332pJWc6RBA393Hk2x5LmzlcDCWkESULPIA+5oegXnFyAecB/333333333333333332hYq+YK7hnaZizASy/bPx6yJaeEwHeodvZnnyWts3UA9YBX333333333333333332FL2q1L7Bdp7qb6IaooRndp6ZuEfdX/F03aQ4U8pVmsJwlf333333333333333332EBE90UY7vbsLKoOqJNya8zAPNG6yTlbUGBcI4ET4hsMupD333333333333333332N4EtQXMr1/5dJ96BbaHvdJ8JOFG3ASpGILVDo+4m6Z+MAf333333333333333330pk6uGEdUR/IN5uKIUzGEEQTroZpfSn+0abrRWo0huR8MgDf3333333333333333kCLpuEkEKajO4JY7Lb9W3Vsj5PZTSCTf3/8A/ZuzimD8/G+I29999999999999999rAAHrmC8jdSfp9GbhmQoE6VbnNRn8Az1UqLDNhSoyTQreLJ19999999999999999+A9LyqCNaI2jCvk9nPhNvXUjXfLXeTa3gEXkgnDSr+qe8BqG9999999999999999sEHrOyDhUqOVb6z1RkIPeJdTyvAb/3BVBpME05uBQuHGqIpF9999999999999999tAhL3rHRMEZTRA+uszTSBf/AHY3wLyuaIgJ5PMGOqYbbWUJgxvfffffffffffffffaxe6+jjLNBOc0XnhDHLsgcp2FBHmom+saemKFqCIch/Nh1jBvfffffffffffffffagbS5XBKFFxU4MNNLdRDIe0TuIrjoiKaBnepC1xh4ua6ndvFvfffffffffffffffSF8XKYPsIGYS9lnGPYTG2JFyABRatkJ36qMwGcos6Y1GFQkxvfffffffffffffffSVlcDBEWLLWdv5JNILb7BqE1NyJoehOQz3kpDVPimFcwxu40/fffffffffffffffQ8gVgctidCbkpz+kDGCDHJslyQur5N6E7NMSOEY7QH0yw3jA/fffffffffffffffY3ck4CyudLbmW31xITCPHJr7tZjmcM87znfTd5dAzdpHYKbB/fffffffffffffffYtYk9xMQgeUpToquPXKIKDK0cxydZImSYrweAGnfVK2X78/UfffffffffffffffbwISdu/XXDrXvaVk7iJHKLfcZn0YRRNoTb432E9899k2l7HZBfffffffffffffffewICVjalpfgVy2cqm8AJKEYxpTWSTMKqEFeUBEyGC086XbUXg/ffffffffffffffegEBr7PhgCxc5Id0gwcEBLS58wRZWaDBCGFCVyw6e2CFhXDvCP/AH33333/xAAC/9oADAMBAAIAAwAAABD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AI3743//AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wA3vc888cv/AM//AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD3+M2uXLN4+7GP/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/LN0HVZ9qsKdqoJev/8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wDH4tly49L9B2yuLC/c/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD7OH0dY8Fqyqkp3gsWL9//AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD9MpJM4kbedjx728wt1Vv/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/o8yuz/3jVSVJ4bPv2H70/8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/APstSLjlvzjpjFvAIi5X/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wDPypuvalVnFGaA0fqYJ6//AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wDPbiCCJ1AM1DiaNfkV/HP/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wDKmGhoTTGOSX82CAz/AJ/z/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8Av6peAwyWwRzTaSdR+Ln/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AH6Xk741LqE7+pZEm1i//wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wB6FKOq8MPD/rvPk07bLP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP13LIka+btSSrc3azktZP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP2OI0rV5DAhtzVuAvXxF/8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8AycAp6kL/AFATudN07m/0/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD27lGmJ9GWUgswdHaC/P8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A+/w5GjPPcZz3USzG2z//AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A0PLSpfXu58kCb03n/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A7LQbSK4XosIcZi7XP/8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/APG796fhtLtekeXvP/8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AN7kwQvsAAijE+1//wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/PxjrJdyPVI9Jh0LPP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/u/XNCNNtlJrcgwP9z/Tf/8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/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" alt="Prasad Sudhir Thorat">
      </div>
      <div class="id-block">
        <h1>Prasad Sudhir Thorat</h1>
        <div class="role">B.Tech (Integrated) CSE · Cybersecurity Enthusiast · Aspiring Software Engineer</div>
        <div class="meta">Sanjivani University, Kopargaon, Maharashtra — 2nd Year</div>
        <p class="tagline">Building a foundation across cybersecurity, cloud infrastructure and applied AI — one certification, workshop and hands-on project at a time.</p>
        <div class="cta-row">
          <a href="Prasad_Thorat_Resume.pdf" download class="btn btn-primary">↓ Download Resume</a>
          <div class="icon-row">
            <a class="icon-btn" href="https://www.linkedin.com/in/prasad-thorat-a38578372" target="_blank" rel="noopener" title="LinkedIn">
              <svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.45 20.45h-3.55v-5.57c0-1.33-.02-3.03-1.85-3.03-1.85 0-2.14 1.45-2.14 2.94v5.66H9.36V9h3.41v1.56h.05c.47-.9 1.63-1.85 3.36-1.85 3.6 0 4.27 2.37 4.27 5.45v6.29zM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12zM7.12 20.45H3.56V9h3.56v11.45z"/></svg>
            </a>
            <a class="icon-btn" href="https://github.com/prasadthorat25uid-arch" target="_blank" rel="noopener" title="GitHub">
              <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.48 2 2 6.58 2 12.21c0 4.51 2.87 8.33 6.84 9.68.5.1.68-.22.68-.49 0-.24-.01-.87-.01-1.71-2.78.62-3.37-1.37-3.37-1.37-.45-1.18-1.11-1.49-1.11-1.49-.9-.63.07-.62.07-.62 1 .07 1.53 1.05 1.53 1.05.89 1.56 2.34 1.11 2.91.85.09-.66.35-1.11.63-1.37-2.22-.26-4.56-1.14-4.56-5.06 0-1.12.39-2.03 1.03-2.75-.1-.26-.45-1.31.1-2.73 0 0 .84-.28 2.75 1.05a9.34 9.34 0 0 1 5 0c1.91-1.33 2.75-1.05 2.75-1.05.55 1.42.2 2.47.1 2.73.64.72 1.03 1.63 1.03 2.75 0 3.93-2.34 4.79-4.57 5.05.36.32.68.94.68 1.9 0 1.37-.01 2.48-.01 2.82 0 .27.18.6.69.49A10.02 10.02 0 0 0 22 12.21C22 6.58 17.52 2 12 2z"/></svg>
            </a>
            <a class="icon-btn" href="https://wa.me/918010989708" target="_blank" rel="noopener" title="WhatsApp">
              <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.87.5 3.62 1.44 5.13L2 22l5.13-1.53a9.85 9.85 0 0 0 4.91 1.31h.01c5.46 0 9.91-4.45 9.91-9.91 0-2.65-1.03-5.14-2.9-7.01A9.83 9.83 0 0 0 12.04 2zm5.8 14.1c-.24.68-1.4 1.33-1.93 1.4-.5.07-1.09.1-1.76-.11a10.9 10.9 0 0 1-1.7-.63c-3-1.29-4.95-4.3-5.1-4.5-.15-.2-1.22-1.62-1.22-3.1s.78-2.19 1.06-2.49c.28-.3.6-.37.8-.37h.58c.19 0 .43-.07.68.51.24.58.83 2.01.9 2.16.07.15.12.32.02.52-.09.2-.14.32-.28.5-.14.18-.29.4-.42.53-.14.14-.28.29-.12.57.16.28.72 1.19 1.55 1.93 1.06.95 1.96 1.24 2.24 1.38.28.14.44.12.6-.07.16-.19.68-.79.87-1.06.18-.27.36-.22.6-.13.24.09 1.5.71 1.76.84.26.13.43.2.5.31.06.11.06.65-.17 1.32z"/></svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </header>

  <!-- ABOUT -->
  <section id="about">
    <div class="section-inner about-grid">
      <div>
        <div class="eyebrow">whoami</div>
        <h2 class="sec-title">About</h2>
        <p>I'm <strong>Prasad Sudhir Thorat</strong>, a second-year Integrated B.Tech Computer Science & Engineering student at <strong>Sanjivani University, Kopargaon</strong>. My focus sits at the intersection of <strong>cybersecurity, cloud infrastructure and applied AI</strong> — I like understanding systems well enough to know where they break.</p>
        <p>Over the past year I completed a hands-on <strong>cybersecurity internship</strong>, worked through cloud labs on AWS ECS, and stacked up certifications across programming, digital forensics and generative AI tooling. I actively share what I learn — recent posts have covered computer networking, IP addressing and subnetting.</p>
        <p>Off the technical track, I stay curious about how AI tools reshape everyday productivity, and I show up for campus life — from hackathon idea pitches to quiz competitions.</p>
      </div>
      <div class="fact-panel">
        <div class="fact-row"><span>institution</span><span>Sanjivani University</span></div>
        <div class="fact-row"><span>program</span><span>B.Tech (Integrated) CSE</span></div>
        <div class="fact-row"><span>status</span><span>2nd Year, In Progress</span></div>
        <div class="fact-row"><span>location</span><span>Kopargaon, Maharashtra</span></div>
        <div class="fact-row"><span>focus</span><span>Cybersecurity · Cloud · AI</span></div>
        <div class="fact-row"><span>internship</span><span>InternsPort Innovation</span></div>
      </div>
    </div>
  </section>

  <!-- SKILLS -->
  <section id="skills">
    <div class="section-inner">
      <div class="eyebrow">stack.json</div>
      <h2 class="sec-title">Skills</h2>
      <div class="skills-grid">
        <div class="skill-card">
          <div class="cat">Languages</div>
          <div class="skill-tags">
            <span class="skill-tag">C</span><span class="skill-tag">Python</span><span class="skill-tag">HTML</span>
          </div>
        </div>
        <div class="skill-card">
          <div class="cat">Cybersecurity</div>
          <div class="skill-tags">
            <span class="skill-tag">Digital Forensics</span><span class="skill-tag">IP Addressing</span><span class="skill-tag">Subnetting</span><span class="skill-tag">Security Fundamentals</span>
          </div>
        </div>
        <div class="skill-card">
          <div class="cat">Cloud & DevOps</div>
          <div class="skill-tags">
            <span class="skill-tag">AWS ECS</span><span class="skill-tag">KodeKloud Labs</span>
          </div>
        </div>
        <div class="skill-card">
          <div class="cat">AI & Tools</div>
          <div class="skill-tags">
            <span class="skill-tag">Claude AI</span><span class="skill-tag">Google Workspace AI</span><span class="skill-tag">Generative AI Studio</span><span class="skill-tag">ChatGPT</span>
          </div>
        </div>
        <div class="skill-card">
          <div class="cat">Productivity</div>
          <div class="skill-tags">
            <span class="skill-tag">Excel (AI-powered)</span><span class="skill-tag">Python Scripting</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- EXPERIENCE -->
  <section id="experience">
    <div class="section-inner">
      <div class="eyebrow">runtime.log</div>
      <h2 class="sec-title">Experience</h2>
      <div class="exp-card">
        <div class="exp-head">
          <div>
            <h3>Cybersecurity Intern</h3>
            <div class="company">InternsPort Innovation Pvt. Ltd.</div>
          </div>
          <div class="date">FEB 2026 — APR 2026</div>
        </div>
        <ul>
          <li>Completed a 2-month internship in the domain of cybersecurity.</li>
          <li>Demonstrated strong analytical thinking, problem-solving ability and effective communication throughout the program.</li>
          <li>Earned a Letter of Recommendation from the Head of Operations.</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- CERTIFICATIONS -->
  <section id="certifications">
    <div class="section-inner">
      <div class="eyebrow">credentials.vault</div>
      <h2 class="sec-title">Certifications</h2>
      <div class="cert-groups">

        <div class="cert-group">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 10h-1.26A8 8 0 1 0 9 20h9a5 5 0 0 0 0-10z"/></svg>
            </div>
            <h3>CLOUD & INFRASTRUCTURE</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">AWS Elastic Container Service (ECS)</span><span class="issuer">KodeKloud</span></li>
            <li class="cert-item"><span class="name">KodeKloud Challenges Completion Certificate</span><span class="issuer">KodeKloud</span></li>
          </ul>
        </div>

        <div class="cert-group">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M16 18l6-6-6-6M8 6l-6 6 6 6"/></svg>
            </div>
            <h3>PROGRAMMING</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">Introduction to Python</span><span class="issuer">Infosys Springboard</span></li>
            <li class="cert-item"><span class="name">Python Fundamentals</span><span class="issuer">Infosys Springboard</span></li>
            <li class="cert-item"><span class="name">Introduction to C</span><span class="issuer">Sololearn</span></li>
            <li class="cert-item"><span class="name">Programming for Beginners: Master the C Language</span><span class="issuer">Learn Programming Academy</span></li>
          </ul>
        </div>

        <div class="cert-group">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M12 1v6M12 17v6M4.2 4.2l4.2 4.2M15.6 15.6l4.2 4.2M1 12h6M17 12h6M4.2 19.8l4.2-4.2M15.6 8.4l4.2-4.2"/></svg>
            </div>
            <h3>ARTIFICIAL INTELLIGENCE & GENAI</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">AI Fluency: AI Capabilities & Limitations</span><span class="issuer">Anthropic</span></li>
            <li class="cert-item"><span class="name">Introduction to Claude Cowork</span><span class="issuer">Anthropic</span></li>
            <li class="cert-item"><span class="name">Claude 101</span><span class="issuer">Anthropic</span></li>
            <li class="cert-item"><span class="name">Bring AI to Work Workshop</span><span class="issuer">Google Workspace</span></li>
            <li class="cert-item"><span class="name">Introduction to Generative AI Studio</span><span class="issuer">Simplilearn</span></li>
            <li class="cert-item"><span class="name">Generative AI Mastery Workshop</span><span class="issuer">NxtWave / OpenAI Academy</span></li>
            <li class="cert-item"><span class="name">AI Tools & ChatGPT Workshop</span><span class="issuer">10X / BeLux</span></li>
            <li class="cert-item"><span class="name">Microsoft Excel Using AI</span><span class="issuer">OfficeMaster</span></li>
          </ul>
        </div>

        <div class="cert-group">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2l8 4v6c0 5-3.5 8.5-8 10-4.5-1.5-8-5-8-10V6l8-4z"/></svg>
            </div>
            <h3>CYBERSECURITY</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">Cybersecurity Mastery</span><span class="issuer">Unstop</span></li>
            <li class="cert-item"><span class="name">Hands-on Digital Forensics & Investigation Workshop</span><span class="issuer">Indian Cyber Club</span></li>
            <li class="cert-item"><span class="name">SEBI Investor Awareness Test</span><span class="issuer">NISM</span></li>
          </ul>
        </div>

        <div class="cert-group">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>
            </div>
            <h3>SOFT SKILLS</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">Communication Skills</span><span class="issuer">MindLuster</span></li>
          </ul>
        </div>

      </div>
    </div>
  </section>

  <!-- ACHIEVEMENTS -->
  <section id="achievements">
    <div class="section-inner">
      <div class="eyebrow">event.history</div>
      <h2 class="sec-title">Events, Workshops & Competitions</h2>
      <div class="timeline">
        <div class="t-item">
          <div class="t-date">SEP 2025</div>
          <h4>Smart India Hackathon (Internal)</h4>
          <p>Sanjivani University — Team "Code Warriors," idea presentation round.</p>
        </div>
        <div class="t-item">
          <div class="t-date">NOV 2025</div>
          <h4>Constitution Day Quiz Competition</h4>
          <p>Sanjivani University — scored 90%.</p>
        </div>
        <div class="t-item">
          <div class="t-date">NOV 2025</div>
          <h4>GenAI Buildathon</h4>
          <p>NxtWave / OpenAI Academy.</p>
        </div>
        <div class="t-item">
          <div class="t-date">DEC 2025</div>
          <h4>Artificial Intelligence Workshop</h4>
          <p>Techfest, IIT Bombay.</p>
        </div>
        <div class="t-item">
          <div class="t-date">2025 — 2026</div>
          <h4>MYBharat Online Quizzes & Dr. B.R. Ambedkar Quiz 2025</h4>
          <p>DFPD-II, Viksit Rajasthan @2047, VBYLD 2026 · Ministry of Social Justice & Empowerment.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact">
    <div class="section-inner contact-panel">
      <div class="eyebrow" style="justify-content:center;">connect</div>
      <h2>Let's build something secure.</h2>
      <p>Open to internships, collaborations and conversations about cybersecurity, cloud and AI.</p>
      <div class="cta-row" style="justify-content:center;">
        <a href="Prasad_Thorat_Resume.pdf" download class="btn btn-primary">↓ Download Resume</a>
        <div class="icon-row">
          <a class="icon-btn" href="https://www.linkedin.com/in/prasad-thorat-a38578372" target="_blank" rel="noopener" title="LinkedIn">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.45 20.45h-3.55v-5.57c0-1.33-.02-3.03-1.85-3.03-1.85 0-2.14 1.45-2.14 2.94v5.66H9.36V9h3.41v1.56h.05c.47-.9 1.63-1.85 3.36-1.85 3.6 0 4.27 2.37 4.27 5.45v6.29zM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12zM7.12 20.45H3.56V9h3.56v11.45z"/></svg>
          </a>
          <a class="icon-btn" href="https://github.com/prasadthorat25uid-arch" target="_blank" rel="noopener" title="GitHub">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.48 2 2 6.58 2 12.21c0 4.51 2.87 8.33 6.84 9.68.5.1.68-.22.68-.49 0-.24-.01-.87-.01-1.71-2.78.62-3.37-1.37-3.37-1.37-.45-1.18-1.11-1.49-1.11-1.49-.9-.63.07-.62.07-.62 1 .07 1.53 1.05 1.53 1.05.89 1.56 2.34 1.11 2.91.85.09-.66.35-1.11.63-1.37-2.22-.26-4.56-1.14-4.56-5.06 0-1.12.39-2.03 1.03-2.75-.1-.26-.45-1.31.1-2.73 0 0 .84-.28 2.75 1.05a9.34 9.34 0 0 1 5 0c1.91-1.33 2.75-1.05 2.75-1.05.55 1.42.2 2.47.1 2.73.64.72 1.03 1.63 1.03 2.75 0 3.93-2.34 4.79-4.57 5.05.36.32.68.94.68 1.9 0 1.37-.01 2.48-.01 2.82 0 .27.18.6.69.49A10.02 10.02 0 0 0 22 12.21C22 6.58 17.52 2 12 2z"/></svg>
          </a>
          <a class="icon-btn" href="https://wa.me/918010989708" target="_blank" rel="noopener" title="WhatsApp">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.87.5 3.62 1.44 5.13L2 22l5.13-1.53a9.85 9.85 0 0 0 4.91 1.31h.01c5.46 0 9.91-4.45 9.91-9.91 0-2.65-1.03-5.14-2.9-7.01A9.83 9.83 0 0 0 12.04 2zm5.8 14.1c-.24.68-1.4 1.33-1.93 1.4-.5.07-1.09.1-1.76-.11a10.9 10.9 0 0 1-1.7-.63c-3-1.29-4.95-4.3-5.1-4.5-.15-.2-1.22-1.62-1.22-3.1s.78-2.19 1.06-2.49c.28-.3.6-.37.8-.37h.58c.19 0 .43-.07.68.51.24.58.83 2.01.9 2.16.07.15.12.32.02.52-.09.2-.14.32-.28.5-.14.18-.29.4-.42.53-.14.14-.28.29-.12.57.16.28.72 1.19 1.55 1.93 1.06.95 1.96 1.24 2.24 1.38.28.14.44.12.6-.07.16-.19.68-.79.87-1.06.18-.27.36-.22.6-.13.24.09 1.5.71 1.76.84.26.13.43.2.5.31.06.11.06.65-.17 1.32z"/></svg>
          </a>
        </div>
      </div>
    </div>
  </section>

  <footer>© 2026 PRASAD_THORAT · SESSION_TERMINATED_SAFELY · Sanjivani University, Kopargaon</footer>

</div>

<script>
  const lines = [
    {text:'> initializing secure_profile.sys', cls:'prompt'},
    {text:'> scanning credentials ... [OK]', cls:'ok'},
    {text:'> loading identity: PRASAD_SUDHIR_THORAT', cls:'ok'},
    {text:'> institution: SANJIVANI_UNIVERSITY, KOPARGAON', cls:'prompt'},
    {text:'> clearance level: STUDENT_DEVELOPER', cls:'ok'},
    {text:'> ACCESS GRANTED', cls:'granted'}
  ];
  const term = document.getElementById('terminal');
  const reveal = document.getElementById('profileReveal');

  function typeLine(idx){
    if(idx >= lines.length){
      setTimeout(()=> reveal.classList.add('show'), 250);
      return;
    }
    const {text, cls} = lines[idx];
    const div = document.createElement('div');
    div.className = 'line ' + cls;
    term.appendChild(div);
    div.style.opacity = 1;
    let i = 0;
    const speed = 18;
    function type(){
      if(i <= text.length){
        div.textContent = text.slice(0,i);
        if(i < text.length){
          div.innerHTML = text.slice(0,i) + '<span class="cursor"></span>';
        }
        i++;
        setTimeout(type, speed);
      } else {
        div.textContent = text;
        setTimeout(()=> typeLine(idx+1), 200);
      }
    }
    type();
  }
  typeLine(0);

  // scroll reveal for sections
  const observer = new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(e.isIntersecting){
        e.target.style.opacity = 1;
        e.target.style.transform = 'translateY(0)';
      }
    });
  },{threshold:0.1});
  document.querySelectorAll('section').forEach(s=>{
    s.style.opacity = 0;
    s.style.transform = 'translateY(24px)';
    s.style.transition = 'opacity .6s ease, transform .6s ease';
    observer.observe(s);
  });
</script>

</body>
</html>
