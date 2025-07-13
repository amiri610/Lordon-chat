# Lordon-chat
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Lordon Chat App</title>
  <link rel="stylesheet" href="style.css" />
  <style>
    /*css
///// */
body, html {
  margin: 0; padding: 0; height: 100%;
  font-family: sans-serif;
  background-color: #f5fff8;
  color: #333;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

#content {
  padding-bottom: 60px; /* ruang untuk tab bar */
  padding-top: 12px;
  overflow-y: auto;
  flex-grow: 1;
}

.chatArea {
  position: fixed;      /* agar chatArea tetap di posisi layar */
  top: 0;               /* mulai dari atas layar */
  left: 0;
  right: 0;
  bottom: 110px;         /* sisakan ruang untuk input dan tab bar */
  overflow-y: auto;
  background: #e5f9f0;  /* warna background chat area */
  padding: 12px;
  box-sizing: border-box;
  z-index: 500;         /* agar di atas konten lain */
}

#chatBox {
  display: flex;
  flex-direction: column;
}

.chat-message {
  margin-bottom: 8px;
  color: #222;
  font-size: 14px;
  cursor: pointer;
}

.chat-message small {
  color: #555;
  font-size: 11px;
  display: block;
  text-align: right;
}

.input-area {
  position: fixed;
  bottom: 60px; /* di atas tab bar */
  left: 0;
  right: 0;
  height: 50px;
  background: #fff;
  display: flex;
  align-items: center;
  padding: 0 10px;
  box-sizing: border-box;
  border-top: 1px solid #ccc;
  z-index: 900;
}

.input-area textarea {
  flex-grow: 1;
  resize: none;
  height: 35px;
  border-radius: 18px;
  border: 1px solid #ccc;
  padding: 5px 12px;
  font-size: 14px;
  outline: none;
  font-family: sans-serif;
}

.input-area button {
  margin-left: 8px;
  background: #2ecc71;
  border: none;
  color: white;
  padding: 8px 14px;
  border-radius: 18px;
  cursor: pointer;
  font-weight: bold;
  font-size: 14px;
  user-select: none;
}

.input-area button:active {
  background: #27ae60;
}

.emoji-btn {
  font-size: 20px;
  margin-right: 8px;
  cursor: pointer;
  user-select: none;
}

.tab-bar {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 60px;
  background: #fff;
  border-top: 1px solid #ccc;
  display: flex;
  justify-content: space-around;
  align-items: center;
  z-index: 1000;
}

.tab {
  flex-grow: 1;
  text-align: center;
  cursor: pointer;
  font-size: 18px;
  color: #333;
  user-select: none;
}

.tab.active {
  color: #2ecc71;
  font-weight: bold;
}

.splash {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  animation: fadeOut 1s ease-out 2s forwards;
}

@keyframes fadeOut {
  to { opacity: 0; visibility: hidden; }
}

.logo {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #2ecc71;
}

.loading {
  font-size: 16px;
  color: #2ecc71;
  animation: blink 1s infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.4; }
}

.footer {
  position: absolute;
  bottom: 10px;
  width: 100%;
  text-align: center;
  font-size: 12px;
  color: gray;
}

.login, .main {
  display: none;
  flex-direction: column;
  flex: 1;
  padding: 20px;
}

.login input {
  padding: 10px;
  margin-bottom: 10px;
  font-size: 16px;
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.login button {
  padding: 10px;
  font-size: 16px;
  background-color: #2ecc71;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.settings {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding-top: 10px;
}

.setting-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #ccc;
  padding: 8px 0;
}

.setting-label {
  font-size: 16px;
}

.setting-toggle {
  width: 50px;
  height: 25px;
  background: #ccc;
  border-radius: 20px;
  position: relative;
  cursor: pointer;
}

.setting-toggle::before {
  content: '';
  position: absolute;
  width: 22px;
  height: 22px;
  background: white;
  border-radius: 50%;
  top: 1.5px;
  left: 2px;
  transition: 0.3s;
}

.setting-toggle.active {
  background: #2ecc71;
}

.setting-toggle.active::before {
  left: 26px;
}

button.setting-button {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}

.chat-time {
  font-size: 11px;
  color: #555;
  margin-top: 2px;
  text-align: right;
}

.chat-text {
  /* tanpa border atau box, hanya teks biasa */
}
  </style>
</head>
<body>

  <!-- Splash Screen -->
  <div class="splash" id="splash">
    <div class="logo">Lordon Chat</div>
    <div class="loading">Memuat...</div>
    <div class="footer">from : Amiri</div>
  </div>

  <!-- Login -->
  <div class="login" id="login">
    <h3>Masukkan Nomor HP Anda</h3>
    <input type="text" id="nomorInput" placeholder="08xxxxxxxxxx" />
    <button onclick="masukApp()">Masuk</button>
  </div>

  <!-- Main App -->
  <div class="main" id="main">
    <div id="content">
      <!-- Konten akan dimuat berdasarkan tab -->
    </div>

    <!-- Kotak Chat hanya muncul di Beranda -->
    <div class="chatArea" style="display: none;">
      <div id="chatBox"></div>
    </div>

    <!-- Input area chat ala WA -->
    <div class="input-area" style="display:none;">
      <div class="emoji-btn" id="emojiBtn" title="Emoji">😊</div>
      <textarea id="inputPesan" placeholder="Ketik pesan..." rows="1"></textarea>
      <button id="btnKirim">Kirim</button>
    </div>

    <!-- Tab Bar -->
    <div class="tab-bar">
      <div class="tab active" data-tab="Beranda" onclick="setTab('Beranda')">🏠<br>Beranda</div>
      <div class="tab" data-tab="Grup" onclick="setTab('Grup')">👥<br>Grup</div>
      <div class="tab" data-tab="Status" onclick="setTab('Status')">📸<br>Status</div>
      <div class="tab" data-tab="Kontak" onclick="setTab('Kontak')">➕<br>Kontak</div>
      <div class="tab" data-tab="Pengaturan" onclick="setTab('Pengaturan')">⚙️<br>Pengaturan</div>
    </div>
  </div>

  <script>
   // Saat halaman dimuat
window.onload = () => {
  const nomor = localStorage.getItem('nomorPengguna');
  const tema = localStorage.getItem('tema');

  // Terapkan tema
  if (tema === 'gelap') {
    document.body.style.backgroundColor = '#222';
    document.body.style.color = '#eee';
  } else {
    document.body.style.backgroundColor = '#f5fff8';
    document.body.style.color = '#333';
  }

  // Splash screen delay
  setTimeout(() => {
    if (nomor) {
      document.getElementById('main').style.display = 'flex';
      setTab('Beranda');  // langsung ke beranda setelah load
    } else {
      document.getElementById('login').style.display = 'flex';
    }
    document.getElementById('splash').style.display = 'none';
  }, 4000);

  // Enter tekan di input login
  const input = document.getElementById('nomorInput');
  if (input) {
    input.addEventListener('keypress', function (e) {
      if (e.key === 'Enter') masukApp();
    });
  }

  // Setup tombol kirim dan emoji
  document.getElementById('btnKirim').addEventListener('click', kirimPesan);
  document.getElementById('inputPesan').addEventListener('keypress', function(e) {
    if (e.key === 'Enter' && !e.shiftKey) {
      e.preventDefault();
      kirimPesan();
    }
  });
  document.getElementById('emojiBtn').addEventListener('click', () => {
    const input = document.getElementById('inputPesan');
    input.value += '😊';
    input.focus();
  });
};

// Login simpan nomor pengguna
function masukApp() {
  const nomor = document.getElementById('nomorInput').value.trim();
  if (nomor) {
    localStorage.setItem('nomorPengguna', nomor);
    document.getElementById('login').style.display = 'none';
    document.getElementById('main').style.display = 'flex';
    setTab('Beranda');
  } else {
    alert("Nomor HP tidak boleh kosong!");
  }
}

// Fungsi utama pindah tab
function setTab(nama) {
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t => {
    if (t.innerText.includes(nama)) t.classList.add('active');
  });

  const content = document.getElementById('content');
  const chatArea = document.querySelector('.chatArea');
  const inputArea = document.querySelector('.input-area');

  if (nama === 'Beranda') {
    content.innerHTML = '';
    if (!content.contains(chatArea)) content.appendChild(chatArea);
    if (!content.contains(inputArea)) content.appendChild(inputArea);
    chatArea.style.display = 'block';
    inputArea.style.display = 'flex';
    tampilkanChat();
  } else {
    if (chatArea) chatArea.style.display = 'none';
    if (inputArea) inputArea.style.display = 'none';

    if (nama === 'Grup') {
      content.innerHTML = '<h3>Daftar Grup</h3>';
    } else if (nama === 'Status') {
      content.innerHTML = '<h3>Status Teman</h3>';
    } else if (nama === 'Kontak') {
      content.innerHTML = `
        <h3>Tambah Kontak</h3>
        <div>
          <input type="text" id="namaKontak" placeholder="Nama kontak" style="width: 100%; padding: 8px; margin-bottom: 8px; box-sizing: border-box;" />
          <input type="text" id="nomorKontak" placeholder="Nomor HP" style="width: 100%; padding: 8px; margin-bottom: 8px; box-sizing: border-box;" />
          <button onclick="tambahKontak()" style="width: 100%; padding: 10px; background: #2ecc71; color: white; border: none; border-radius: 5px; cursor: pointer;">Simpan Kontak</button>
        </div>
        <h4>Daftar Kontak</h4>
        <ul id="daftarKontak" style="list-style: none; padding-left: 0;"></ul>
      `;
      tampilkanKontak();
    } else if (nama === 'Pengaturan') {
      content.innerHTML = `
        <h3>Pengaturan Akun</h3>
        <div class="settings">
          <div class="setting-item">
            <div class="setting-label">Tema Gelap</div>
            <div class="setting-toggle" onclick="toggleTema(this)" id="temaToggle"></div>
          </div>
          <div class="setting-item">
            <div class="setting-label">Notifikasi</div>
            <div class="setting-toggle" onclick="toggleNotifikasi(this)" id="notifikasiToggle"></div>
          </div>
          <button class="setting-button" onclick="hapusChat()">Hapus Semua Chat</button>
          <button class="setting-button" onclick="logout()">Logout</button>
          <p style="font-size:12px; color:gray; text-align:center;">Versi 1.0.0<br>by Mhd_Amiri_Hsn</p>
        </div>
      `;
      document.getElementById('temaToggle').classList.toggle('active', localStorage.getItem('tema') === 'gelap');
      document.getElementById('notifikasiToggle').classList.toggle('active', localStorage.getItem('notifikasi') === 'on');
    }
  }
}

// Tambah kontak ke localStorage
function tambahKontak() {
  const nama = document.getElementById('namaKontak').value.trim();
  const nomor = document.getElementById('nomorKontak').value.trim();
  if (!nama || !nomor) {
    alert('Nama dan Nomor harus diisi!');
    return;
  }

  let kontakList = JSON.parse(localStorage.getItem('kontakList') || '[]');
  kontakList.push({ nama, nomor });
  localStorage.setItem('kontakList', JSON.stringify(kontakList));

  document.getElementById('namaKontak').value = '';
  document.getElementById('nomorKontak').value = '';
  tampilkanKontak();
}

// Tampilkan daftar kontak
function tampilkanKontak() {
  const daftar = document.getElementById('daftarKontak');
  if (!daftar) return;
  let kontakList = JSON.parse(localStorage.getItem('kontakList') || '[]');

  daftar.innerHTML = '';
  if (kontakList.length === 0) {
    daftar.innerHTML = '<li>Belum ada kontak.</li>';
    return;
  }

  kontakList.forEach((kontak, index) => {
    const li = document.createElement('li');
    li.style.padding = '6px 0';
    li.style.borderBottom = '1px solid #ccc';
    li.innerHTML = `
      <strong>${kontak.nama}</strong><br>
      <small style="cursor:pointer; color:#2ecc71;" onclick="kirimLangsung('${kontak.nomor}', '${kontak.nama}')">${kontak.nomor}</small>
      <button onclick="hapusKontak(${index})" style="float:right; background:#e74c3c; color:white; border:none; border-radius:3px;">Hapus</button>
    `;
    daftar.appendChild(li);
  });
}

// Hapus kontak
function hapusKontak(index) {
  let kontakList = JSON.parse(localStorage.getItem('kontakList') || '[]');
  kontakList.splice(index, 1);
  localStorage.setItem('kontakList', JSON.stringify(kontakList));
  tampilkanKontak();
}

// Lanjutan fungsi kirimLangsung dari daftar kontak
function kirimLangsung(nomor, nama) {
  const pesan = prompt(`Ketik pesan untuk ${nama} (${nomor}):`);
  if (pesan) {
    let chat = JSON.parse(localStorage.getItem('chatData') || '[]');
    chat.push({
      isi: `📩 ke ${nama} (${nomor}): ${pesan}`,
      waktu: new Date().toLocaleTimeString()
    });
    localStorage.setItem('chatData', JSON.stringify(chat));
    setTab('Beranda'); // langsung tampilkan tab Beranda setelah kirim
  }
}

// Tampilkan chat di beranda
function tampilkanChat() {
  const chatBox = document.getElementById('chatBox');
  const chat = JSON.parse(localStorage.getItem('chatData') || '[]');
  chatBox.innerHTML = '';

  chat.forEach((item, index) => {
    const div = document.createElement('div');
    div.classList.add('chat-message');
    div.dataset.index = index;
    div.style.background = 'transparent';
    div.style.padding = '0';
    div.style.boxShadow = 'none';
    div.style.borderRadius = '0';
    div.style.marginBottom = '8px';

    div.innerHTML = `
      <small>${item.waktu}</small><br>
      <span>${item.isi}</span>
    `;

    // Klik pesan akan mengisi textarea untuk reply (contoh sederhana)
    div.addEventListener('click', () => {
      const inputPesan = document.getElementById('inputPesan');
      inputPesan.value = `Balas: ${item.isi}\n`;
      inputPesan.focus();
    });

    chatBox.appendChild(div);
  });

  chatBox.scrollTop = chatBox.scrollHeight;
}

// Kirim pesan dari input area
function kirimPesan() {
  const input = document.getElementById('inputPesan');
  const isi = input.value.trim();
  if (!isi) return alert('Pesan tidak boleh kosong!');

  let chat = JSON.parse(localStorage.getItem('chatData') || '[]');
  chat.push({
    isi,
    waktu: new Date().toLocaleTimeString()
  });
  localStorage.setItem('chatData', JSON.stringify(chat));
  input.value = '';
  tampilkanChat();
}

// Pengaturan tema
function toggleTema(el) {
  const aktif = el.classList.toggle('active');
  localStorage.setItem('tema', aktif ? 'gelap' : 'terang');
  document.body.style.backgroundColor = aktif ? '#222' : '#f5fff8';
  document.body.style.color = aktif ? '#eee' : '#333';
}

// Pengaturan notifikasi
function toggleNotifikasi(el) {
  const aktif = el.classList.toggle('active');
  localStorage.setItem('notifikasi', aktif ? 'on' : 'off');
  alert("Notifikasi " + (aktif ? "diaktifkan" : "dinonaktifkan"));
}

// Hapus semua chat
function hapusChat() {
  if (confirm("Yakin ingin menghapus semua pesan?")) {
    localStorage.removeItem('chatData');
    alert("Chat berhasil dihapus.");
    if(document.querySelector('.tab.active')?.innerText.includes('Beranda')) {
      tampilkanChat();
    }
  }
}

// Logout aplikasi
function logout() {
  if (confirm("Keluar dari aplikasi?")) {
    localStorage.removeItem('nomorPengguna');
    location.reload();
  }
}
</script>
</body>
</html>
