<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ระบบติดตามงานและคะแนนนักเรียน (Real-time)</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts: Prompt & FontAwesome -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- MQTT.js สำหรับ Real-Time Cloud Sync ทันทีโดยไม่ต้องมีเซิร์ฟเวอร์ส่วนตัว -->
  <script src="https://unpkg.com/mqtt/dist/mqtt.min.js"></script>

  <style>
    body {
      font-family: 'Prompt', sans-serif;
      background: linear-gradient(135deg, #f0fdf4 0%, #e0f2fe 50%, #faf5ff 100%);
      min-height: 100vh;
    }
  </style>
</head>
<body class="text-slate-700 pb-16">

  <!-- แถบสถานะการเชื่อมต่อ Real-time -->
  <div id="connection-status-bar" class="py-1 px-4 text-xs font-medium text-center transition-colors duration-300 bg-amber-500 text-white flex items-center justify-center gap-2">
    <span class="w-2 h-2 rounded-full bg-white animate-ping"></span>
    <span id="connection-status-text">กำลังเชื่อมต่อไปยังห้องเรียน Real-time...</span>
  </div>

  <!-- Navbar -->
  <nav class="bg-white/80 backdrop-blur-md border-b border-slate-200 px-4 py-3 sticky top-0 z-30 shadow-sm">
    <div class="max-w-5xl mx-auto flex items-center justify-between">
      <div class="flex items-center gap-2">
        <div class="w-9 h-9 rounded-xl bg-indigo-600 text-white flex items-center justify-center font-bold shadow-md shadow-indigo-200">
          <i class="fa-solid fa-graduation-cap"></i>
        </div>
        <div>
          <span class="font-bold text-slate-800 text-sm sm:text-base block leading-tight">ระบบติดตามงานออนไลน์</span>
          <span id="nav-teacher-title" class="text-[11px] text-slate-400">คุณครู: ยังไม่ได้ระบุ</span>
        </div>
      </div>

      <div class="flex items-center gap-2">
        <div id="user-badge" class="flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-semibold bg-indigo-50 text-indigo-700 border border-indigo-100">
          กำลังโหลด...
        </div>
        <button onclick="openLoginModal()" class="px-3 py-1.5 text-xs font-medium text-slate-600 bg-slate-100 hover:bg-slate-200 rounded-xl transition-all flex items-center gap-1.5">
          <i class="fa-solid fa-arrow-right-arrow-left"></i>
          <span>สลับบทบาท / ห้อง</span>
        </button>
      </div>
    </div>
  </nav>

  <div class="max-w-5xl mx-auto px-4 pt-6">

    <!-- ==================== ฝั่งคุณครูผู้สอน ==================== -->
    <div id="teacher-control-bar" class="hidden space-y-4 mb-6">
      
      <!-- การ์ดห้องเรียนและปุ่มแชร์ลิงก์ให้นักเรียน -->
      <div class="bg-gradient-to-r from-indigo-600 via-purple-600 to-indigo-700 rounded-3xl p-5 shadow-xl text-white">
        <div class="flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
          <div>
            <div class="flex items-center gap-2">
              <span class="px-2.5 py-0.5 rounded-full bg-white/20 text-white text-[11px] font-semibold tracking-wider">โหมดครูผู้สอน</span>
              <span class="text-xs bg-emerald-400/30 text-emerald-100 px-2.5 py-0.5 rounded-full border border-emerald-300/30 flex items-center gap-1">
                <span class="w-1.5 h-1.5 rounded-full bg-emerald-300 animate-pulse"></span> เชื่อมต่อเรียลไทม์
              </span>
            </div>
            <h2 class="text-xl font-bold mt-1.5 flex items-center gap-2">
              ห้องเรียนของ: <span id="teacher-name-display" class="underline decoration-indigo-300">ครู...</span>
            </h2>
            <p class="text-indigo-100 text-xs mt-0.5">
              รหัสห้อง: <span id="teacher-room-code-badge" class="font-mono bg-white/20 px-2 py-0.5 rounded font-bold">---</span> 
              • เมื่อนักเรียนลงชื่อเข้าใช้ จะแสดงบนหน้านี้ทันทีอัตโนมัติ
            </p>
          </div>
          
          <div class="flex flex-wrap items-center gap-2 w-full md:w-auto">
            <button onclick="copyStudentShareLink()" class="flex-1 md:flex-initial px-3.5 py-2 bg-indigo-500/50 hover:bg-indigo-500 border border-white/20 text-white rounded-xl text-xs font-medium transition-all flex items-center justify-center gap-1.5">
              <i class="fa-solid fa-share-nodes"></i> คัดลอกลิงก์ให้นักเรียน
            </button>
            <button onclick="switchTeacherView('roster')" class="px-4 py-2 bg-white text-indigo-700 font-semibold rounded-xl text-xs shadow-sm transition-all flex items-center justify-center gap-1.5">
              <i class="fa-solid fa-users"></i> รายชื่อทั้งหมด (<span id="teacher-student-count">0</span>)
            </button>
            <button onclick="openModal()" class="px-4 py-2 bg-emerald-500 hover:bg-emerald-600 text-white font-medium rounded-xl text-xs shadow-md transition-all flex items-center justify-center gap-1.5">
              <i class="fa-solid fa-plus"></i> เพิ่มงานให้นักเรียน
            </button>
          </div>
        </div>
      </div>

      <!-- กล่องแสดงรายชื่อนักเรียนทุกคนที่เชื่อมต่อเข้ามา -->
      <div id="teacher-roster-view" class="bg-white/90 backdrop-blur-md rounded-3xl p-6 shadow-xl border border-white/60">
        <div class="flex items-center justify-between pb-4 mb-4 border-b border-slate-100">
          <div>
            <h3 class="font-bold text-slate-800 text-base sm:text-lg flex items-center gap-2">
              <i class="fa-solid fa-address-book text-indigo-500"></i> นักเรียนในห้องเรียนนี้ (<span id="teacher-student-count-2">0</span> คน)
            </h3>
            <p class="text-xs text-slate-400 mt-0.5">แตะที่การ์ดนักเรียนเพื่อตรวจงาน และให้คะแนน</p>
          </div>
          <button onclick="openStudentRegistrationModal(false)" class="px-3 py-1.5 bg-indigo-50 hover:bg-indigo-100 text-indigo-600 rounded-xl text-xs font-medium transition-all flex items-center gap-1">
            <i class="fa-solid fa-user-plus text-[11px]"></i> ครูช่วยเพิ่มนักเรียน
          </button>
        </div>

        <div id="teacher-students-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3.5"></div>

        <!-- หน้าว่าง กรณียังไม่มีเด็กเข้าห้อง -->
        <div id="teacher-empty-students" class="hidden flex-col items-center justify-center p-8 text-center">
          <div class="w-14 h-14 rounded-full bg-indigo-50 text-indigo-400 flex items-center justify-center text-2xl mb-2">
            <i class="fa-solid fa-qrcode"></i>
          </div>
          <p class="font-semibold text-slate-700 text-sm">ยังไม่มีนักเรียนเข้าสู่ระบบในห้องนี้</p>
          <p class="text-xs text-slate-400 mt-1 max-w-sm">
            กดปุ่ม <span class="text-indigo-600 font-semibold">"คัดลอกลิงก์ให้นักเรียน"</span> ด้านบน ส่งให้นักเรียนทางแชต หรือให้นักเรียนกรอกรหัสห้องนี้เพื่อลงทะเบียน
          </p>
        </div>
      </div>
    </div>

    <!-- ==================== ส่วนแสดงผลของนักเรียน / งานรายบุคคล ==================== -->
    <div id="student-detail-wrapper">
      <div id="teacher-back-btn-box" class="hidden mb-3">
        <button onclick="switchTeacherView('roster')" class="px-3 py-1.5 bg-white border border-slate-200 hover:bg-slate-50 text-slate-700 text-xs font-semibold rounded-xl shadow-sm transition-all flex items-center gap-1.5">
          <i class="fa-solid fa-chevron-left text-[10px]"></i> ย้อนกลับไปหน้ารายชื่อนักเรียนทั้งหมด
        </button>
      </div>

      <!-- 1. การ์ดโปรไฟล์นักเรียน -->
      <div class="bg-white/80 backdrop-blur-md rounded-3xl p-6 shadow-xl border border-white/40 mb-6 transition-all">
        <div class="flex flex-col sm:flex-row items-center gap-6">
          <div class="relative group cursor-pointer" onclick="triggerAvatarUpload()">
            <div class="w-24 h-24 sm:w-28 sm:h-28 rounded-full ring-4 ring-indigo-300 ring-offset-2 overflow-hidden shadow-inner bg-slate-100 flex items-center justify-center text-slate-400">
              <img id="profile-img" src="" alt="Avatar" class="w-full h-full object-cover hidden">
              <i id="profile-placeholder-icon" class="fa-solid fa-user text-4xl"></i>
            </div>
            <div class="absolute inset-0 bg-black/40 rounded-full flex items-center justify-center text-white opacity-0 group-hover:opacity-100 transition-opacity">
              <i class="fa-solid fa-camera text-xl"></i>
            </div>
            <input type="file" id="avatar-input" accept="image/*" class="hidden" onchange="changeAvatar(event)">
          </div>

          <div class="flex-1 text-center sm:text-left">
            <div class="flex items-center justify-center sm:justify-start gap-2">
              <h1 id="display-name" class="text-2xl sm:text-3xl font-bold text-slate-800">กำลังโหลดข้อมูล...</h1>
              <button id="btn-edit-student-profile" onclick="openStudentRegistrationModal(true)" class="text-indigo-500 hover:text-indigo-600 p-1" title="แก้ไขข้อมูล">
                <i class="fa-solid fa-pen-to-square"></i>
              </button>
            </div>
            <p id="display-class" class="text-slate-500 font-medium text-sm mt-1">ห้อง / เลขที่</p>
            <div class="flex flex-wrap items-center justify-center sm:justify-start gap-2 mt-3">
              <span id="role-tag" class="px-3 py-1 bg-indigo-50 text-indigo-600 rounded-full text-xs font-semibold">
                สถานะ: นักเรียน
              </span>
              <span id="student-notice" class="text-xs text-emerald-700 bg-emerald-50 px-2.5 py-1 rounded-full border border-emerald-200">
                <i class="fa-solid fa-signal text-[10px] mr-1"></i> ซิงค์สดกับคุณครู
              </span>
            </div>
          </div>
        </div>
      </div>

      <!-- 2. Dashboard สรุปงานและคะแนน -->
      <div class="grid grid-cols-2 sm:grid-cols-4 gap-4 mb-6">
        <div class="bg-gradient-to-br from-blue-500 to-cyan-400 text-white p-4 rounded-2xl shadow-lg shadow-blue-100 flex flex-col items-center justify-center">
          <span class="text-xs font-medium opacity-90">งานทั้งหมด</span>
          <span id="stat-total" class="text-3xl font-extrabold mt-1">0</span>
          <span class="text-[10px] mt-1 opacity-75">ชิ้นงาน</span>
        </div>
        <div class="bg-gradient-to-br from-rose-500 to-orange-400 text-white p-4 rounded-2xl shadow-lg shadow-rose-100 flex flex-col items-center justify-center">
          <span class="text-xs font-medium opacity-90">งานค้าง</span>
          <span id="stat-pending" class="text-3xl font-extrabold mt-1">0</span>
          <span class="text-[10px] mt-1 opacity-75">ยังไม่เสร็จ</span>
        </div>
        <div class="bg-gradient-to-br from-emerald-500 to-teal-400 text-white p-4 rounded-2xl shadow-lg shadow-emerald-100 flex flex-col items-center justify-center">
          <span class="text-xs font-medium opacity-90">ส่งแล้ว</span>
          <span id="stat-completed" class="text-3xl font-extrabold mt-1">0</span>
          <span class="text-[10px] mt-1 opacity-75">ตรวจเรียบร้อย</span>
        </div>
        <div class="bg-gradient-to-br from-amber-500 to-yellow-400 text-white p-4 rounded-2xl shadow-lg shadow-amber-100 flex flex-col items-center justify-center">
          <span class="text-xs font-medium opacity-90">คะแนนสะสม</span>
          <span id="stat-score" class="text-3xl font-extrabold mt-1">0/0</span>
          <span class="text-[10px] mt-1 opacity-75">ได้จริง/เต็ม</span>
        </div>
      </div>

      <!-- 3. แท็บกรองสถานะ -->
      <div class="flex items-center justify-between gap-2 mb-4">
        <div class="flex bg-slate-200/70 p-1 rounded-2xl text-xs sm:text-sm font-medium">
          <button onclick="filterTasks('all')" id="tab-all" class="px-3 sm:px-4 py-1.5 rounded-xl bg-white text-indigo-600 shadow-sm transition-all">ทั้งหมด</button>
          <button onclick="filterTasks('pending')" id="tab-pending" class="px-3 sm:px-4 py-1.5 rounded-xl text-slate-600 hover:text-slate-900 transition-all">ค้างอยู่</button>
          <button onclick="filterTasks('completed')" id="tab-completed" class="px-3 sm:px-4 py-1.5 rounded-xl text-slate-600 hover:text-slate-900 transition-all">เสร็จแล้ว</button>
        </div>
        <span id="task-count-label" class="text-xs text-slate-500">แสดงผล 0 รายการ</span>
      </div>

      <!-- 4. รายการงาน -->
      <div id="tasks-container" class="space-y-3"></div>

      <div id="empty-state" class="hidden flex-col items-center justify-center p-12 text-center bg-white/50 rounded-3xl border border-dashed border-slate-300">
        <div class="w-16 h-16 rounded-full bg-indigo-50 text-indigo-400 flex items-center justify-center text-2xl mb-3">
          <i class="fa-regular fa-folder-open"></i>
        </div>
        <p class="text-slate-600 font-semibold" id="empty-state-title">ไม่มีรายการงานในหมวดนี้</p>
        <p id="empty-state-sub" class="text-slate-400 text-sm mt-1"></p>
      </div>
    </div>
  </div>

  <!-- Modal สำหรับเลือกบทบาท / ลงชื่อเข้าใช้ -->
  <div id="login-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4">
    <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-2xl">
      <div class="text-center mb-6">
        <div class="w-14 h-14 bg-indigo-50 text-indigo-600 rounded-2xl flex items-center justify-center text-2xl mx-auto mb-3 shadow-inner">
          <i class="fa-solid fa-chalkboard-user"></i>
        </div>
        <h3 class="text-xl font-bold text-slate-800">ระบบติดตามงานห้องเรียน</h3>
        <p class="text-xs text-slate-500 mt-1">กรุณาเลือกบทบาทในการเข้าสู่ระบบ</p>
      </div>

      <div class="flex bg-slate-100 p-1 rounded-2xl mb-5">
        <button type="button" onclick="switchLoginTab('student')" id="btn-tab-student" class="flex-1 py-2 rounded-xl text-sm font-semibold transition-all bg-white text-indigo-600 shadow-sm">
          <i class="fa-solid fa-user-graduate mr-1"></i> นักเรียน
        </button>
        <button type="button" onclick="switchLoginTab('teacher')" id="btn-tab-teacher" class="flex-1 py-2 rounded-xl text-sm font-semibold transition-all text-slate-500 hover:text-slate-800">
          <i class="fa-solid fa-chalkboard-user mr-1"></i> คุณครูผู้สอน
        </button>
      </div>

      <!-- ฟอร์มเข้าใช้ของนักเรียน -->
      <div id="student-login-section" class="space-y-4">
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">รหัสห้องเรียน / ชื่อห้องของคุณครู *</label>
          <input type="text" id="login-student-room-code" placeholder="เช่น KRU-01" class="w-full px-3 py-2.5 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm uppercase font-mono">
        </div>

        <div id="student-select-wrapper">
          <label class="block text-xs font-semibold text-slate-600 mb-1">เลือกชื่อของตนเอง (กรณีเคยลงทะเบียนแล้ว):</label>
          <select id="login-student-select" class="w-full px-3 py-2.5 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm font-medium bg-slate-50">
            <option value="">-- ยังไม่มีรายชื่อในเครื่องนี้ --</option>
          </select>
        </div>

        <div class="flex flex-col gap-2 pt-1">
          <button onclick="loginAsStudentExisting()" id="btn-login-student-exist" class="w-full py-2.5 bg-indigo-600 hover:bg-indigo-700 text-white font-medium rounded-xl text-sm shadow-md transition-all">
            เข้าใช้งานด้วยชื่อเดิม
          </button>
          <button onclick="openStudentRegistrationModal(false)" class="w-full py-2.5 bg-emerald-50 hover:bg-emerald-100 text-emerald-700 border border-emerald-200 font-medium rounded-xl text-sm transition-all flex items-center justify-center gap-1.5">
            <i class="fa-solid fa-user-plus text-xs"></i> นักเรียนใหม่: ลงทะเบียนชื่อตนเอง
          </button>
        </div>
      </div>

      <!-- ฟอร์มเข้าใช้ของคุณครู -->
      <div id="teacher-login-section" class="hidden space-y-4">
        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">ชื่อ - นามสกุลคุณครู *</label>
          <input type="text" id="teacher-login-name" placeholder="เช่น คุณครูกานดา สดใส" class="w-full px-3 py-2.5 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm font-medium">
        </div>

        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">ตั้งรหัสห้องเรียน (ให้นักเรียนใช้เข้าห้อง) *</label>
          <input type="text" id="teacher-login-room" placeholder="เช่น KRU-MATH-1" class="w-full px-3 py-2.5 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm font-mono uppercase">
        </div>

        <button onclick="loginAsTeacherSubmit()" class="w-full py-3 bg-gradient-to-r from-indigo-600 to-purple-600 hover:opacity-95 text-white font-semibold rounded-xl text-sm shadow-md transition-all">
          เข้าสู่ระบบห้องเรียนคุณครู
        </button>
      </div>
    </div>
  </div>

  <!-- Modal สำหรับนักเรียนลงทะเบียนข้อมูลตัวเอง -->
  <div id="register-student-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-2xl">
      <div class="flex items-center justify-between pb-3 border-b border-slate-100 mb-4">
        <h3 class="text-lg font-bold text-slate-800" id="register-modal-title">กรอกข้อมูลนักเรียน</h3>
        <button onclick="closeStudentRegistrationModal()" class="text-slate-400 hover:text-slate-600">
          <i class="fa-solid fa-xmark text-lg"></i>
        </button>
      </div>

      <form id="register-form" onsubmit="handleSaveStudentProfile(event)" class="space-y-4">
        <div class="flex flex-col items-center justify-center">
          <div class="relative group cursor-pointer" onclick="document.getElementById('reg-avatar-input').click()">
            <div class="w-20 h-20 rounded-full ring-2 ring-indigo-200 overflow-hidden bg-slate-100 flex items-center justify-center text-slate-400">
              <img id="reg-avatar-preview" src="" alt="" class="w-full h-full object-cover hidden">
              <i id="reg-avatar-icon" class="fa-solid fa-camera text-2xl"></i>
            </div>
            <input type="file" id="reg-avatar-input" accept="image/*" class="hidden" onchange="previewRegisterAvatar(event)">
          </div>
          <span class="text-[11px] text-slate-400 mt-1">คลิกเพื่ออัปโหลดรูปโปรไฟล์ (ไม่ใส่ก็ได้)</span>
        </div>

        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">ชื่อ - นามสกุล *</label>
          <input type="text" id="reg-name" required placeholder="เช่น ด.ช. ณัฐวุฒิ สุขสบาย" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm">
        </div>

        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">ชั้น / ห้อง *</label>
            <input type="text" id="reg-room" required placeholder="เช่น ม.2/1 หรือ ป.6" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm">
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">เลขที่</label>
            <input type="text" id="reg-number" placeholder="เช่น 05 หรือ 12" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm">
          </div>
        </div>

        <div class="pt-2 flex gap-3">
          <button type="button" onclick="closeStudentRegistrationModal()" class="flex-1 py-2.5 bg-slate-100 text-slate-600 rounded-xl font-medium text-sm hover:bg-slate-200">ยกเลิก</button>
          <button type="submit" class="flex-1 py-2.5 bg-indigo-600 text-white rounded-xl font-medium text-sm hover:bg-indigo-700 shadow-md">บันทึก & เข้าสู่ระบบ</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Modal สำหรับ ครู มอบหมายงาน / ตรวจให้คะแนน -->
  <div id="task-modal" class="fixed inset-0 bg-slate-900/40 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
    <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-2xl">
      <div class="flex items-center justify-between pb-3 border-b border-slate-100">
        <h3 class="text-lg font-bold text-slate-800" id="modal-title">เพิ่มงานใหม่</h3>
        <button onclick="closeModal()" class="text-slate-400 hover:text-slate-600">
          <i class="fa-solid fa-xmark text-lg"></i>
        </button>
      </div>

      <form id="task-form" onsubmit="saveTask(event)" class="mt-4 space-y-4">
        <input type="hidden" id="task-id">

        <div id="modal-assign-student-box">
          <label class="block text-xs font-semibold text-slate-600 mb-1">มอบหมายให้นักเรียน *</label>
          <select id="modal-student-target" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm font-medium bg-slate-50">
          </select>
        </div>

        <div>
          <label class="block text-xs font-semibold text-slate-600 mb-1">ชื่องาน / รายละเอียดงาน *</label>
          <input type="text" id="task-title" required placeholder="เช่น ใบงานวิชาคณิตศาสตร์ เรื่องเศษส่วน" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm">
        </div>

        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">วิชา</label>
            <input type="text" id="task-subject" placeholder="เช่น วิทยาศาสตร์" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm">
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">กำหนดส่ง</label>
            <input type="date" id="task-deadline" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm">
          </div>
        </div>

        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">คะแนนเต็ม</label>
            <input type="number" step="0.5" id="task-max-score" min="0" placeholder="เช่น 10" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm">
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-600 mb-1">คะแนนที่ได้ (ครูให้คะแนน)</label>
            <input type="number" step="0.5" id="task-score" min="0" placeholder="เช่น 9" class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-400 text-sm">
          </div>
        </div>

        <div class="flex items-center gap-2 pt-1">
          <input type="checkbox" id="task-completed-checkbox" class="w-4 h-4 text-indigo-600 rounded border-slate-300 focus:ring-indigo-500">
          <label for="task-completed-checkbox" class="text-xs font-semibold text-slate-700 cursor-pointer">ตรวจแล้ว / ส่งครบแล้ว</label>
        </div>

        <div class="pt-2 flex gap-3">
          <button type="button" onclick="closeModal()" class="flex-1 py-2.5 bg-slate-100 text-slate-600 rounded-xl font-medium text-sm hover:bg-slate-200">ยกเลิก</button>
          <button type="submit" class="flex-1 py-2.5 bg-indigo-600 text-white rounded-xl font-medium text-sm hover:bg-indigo-700 shadow-md">บันทึก & ซิงค์ข้อมูล</button>
        </div>
      </form>
    </div>
  </div>

  <!-- JavaScript Real-Time Engine -->
  <script>
    // ดึงค่า URL Parameter กรณีเข้าผ่านลิงก์แชร์ เช่น ?room=KRU-01
    const urlParams = new URLSearchParams(window.location.search);
    const roomParam = urlParams.get('room');

    let teacherName = localStorage.getItem('app_teacher_name') || 'ครูประจำวิชา';
    let currentRoomCode = (roomParam || localStorage.getItem('app_room_code') || 'ROOM101').trim().toUpperCase();
    let currentUserRole = localStorage.getItem('app_user_role') || null; // 'teacher' | 'student'
    let currentStudentId = localStorage.getItem('app_current_student_id') || null;
    let studentsData = JSON.parse(localStorage.getItem('app_cached_students_' + currentRoomCode)) || [];
    let teacherCurrentView = 'roster';
    let currentFilter = 'all';
    let tempAvatarBase64 = null;
    let isEditingProfile = false;

    // ระบบ Real-Time Cloud MQTT WebSocket
    let mqttClient = null;
    const MQTT_BROKER_URL = 'wss://broker.emqx.io:8084/mqtt'; // Public Free WebSocket Broker

    function getBaseTopic() {
      // แปลงชื่อห้องให้เป็น Topic ปลอดภัย
      const safeRoom = encodeURIComponent(currentRoomCode).replace(/%/g, '_');
      return `schoolsync_v3/${safeRoom}`;
    }

    function initRealtimeSync() {
      const statusEl = document.getElementById('connection-status-bar');
      const textEl = document.getElementById('connection-status-text');

      try {
        if (mqttClient) mqttClient.end();

        mqttClient = mqtt.connect(MQTT_BROKER_URL, {
          clientId: 'client_' + Math.random().toString(16).substr(2, 8),
          clean: true,
          connectTimeout: 5000
        });

        mqttClient.on('connect', () => {
          statusEl.className = "py-1 px-4 text-xs font-medium text-center transition-colors duration-300 bg-emerald-500 text-white flex items-center justify-center gap-2";
          textEl.innerHTML = `<i class="fa-solid fa-wifi mr-1"></i> เชื่อมต่อ Real-time ห้อง [${currentRoomCode}] เรียบร้อย ข้อมูลซิงค์สดอัตโนมัติ`;

          // Subscribe ข้อมูลในห้องนี้
          const topic = `${getBaseTopic()}/#`;
          mqttClient.subscribe(topic, { qos: 1 });

          // ถ้าเป็นครู ให้บรอดแคสต์ชื่อครูส่งให้นักเรียนในห้อง
          if (currentUserRole === 'teacher') {
            broadcastTeacherInfo();
          }
        });

        mqttClient.on('message', (topic, payload) => {
          try {
            const data = JSON.parse(payload.toString());
            handleRealtimeMessage(topic, data);
          } catch (e) {
            console.error("MQTT parse error", e);
          }
        });

        mqttClient.on('error', (err) => {
          console.warn("MQTT connection error", err);
          statusEl.className = "py-1 px-4 text-xs font-medium text-center bg-amber-500 text-white flex items-center justify-center gap-2";
          textEl.textContent = "เชื่อมต่อเน็ตขัดข้อง: กำลังทำงานในโหมดออฟไลน์และพยายามเชื่อมต่อใหม่...";
        });

      } catch (err) {
        console.warn("Failed to initialize MQTT", err);
      }
    }

    function handleRealtimeMessage(topic, data) {
      const base = getBaseTopic();

      // เมื่อครูประกาศชื่อครู
      if (topic === `${base}/teacher_info`) {
        if (data.teacherName) {
          teacherName = data.teacherName;
          localStorage.setItem('app_teacher_name', teacherName);
          updateTeacherDisplay();
        }
        return;
      }

      // เมื่อมีข้อมูลนักเรียนอัปเดต (นักเรียนลงทะเบียนใหม่ / ครูตรวจงาน)
      if (topic.startsWith(`${base}/students/`)) {
        const studentId = data.id;
        const index = studentsData.findIndex(s => s.id === studentId);

        if (index !== -1) {
          studentsData[index] = data;
        } else {
          studentsData.push(data);
        }

        saveToLocalStorage();
        populateStudentSelects();
        renderAppView();
      }
    }

    // ฟังก์ชันส่งข้อมูลขึ้น Cloud
    function broadcastStudent(student) {
      if (mqttClient && mqttClient.connected) {
        const topic = `${getBaseTopic()}/students/${student.id}`;
        mqttClient.publish(topic, JSON.stringify(student), { retain: true, qos: 1 });
      }
    }

    function broadcastTeacherInfo() {
      if (mqttClient && mqttClient.connected) {
        const topic = `${getBaseTopic()}/teacher_info`;
        mqttClient.publish(topic, JSON.stringify({ teacherName: teacherName }), { retain: true, qos: 1 });
      }
    }

    function saveToLocalStorage() {
      localStorage.setItem('app_cached_students_' + currentRoomCode, JSON.stringify(studentsData));
      localStorage.setItem('app_teacher_name', teacherName);
      localStorage.setItem('app_room_code', currentRoomCode);
      localStorage.setItem('app_user_role', currentUserRole);
      localStorage.setItem('app_current_student_id', currentStudentId);
    }

    function updateTeacherDisplay() {
      document.getElementById('nav-teacher-title').textContent = `คุณครู: ${teacherName} (${currentRoomCode})`;
      document.getElementById('teacher-name-display').textContent = teacherName;
      document.getElementById('teacher-room-code-badge').textContent = currentRoomCode;
    }

    // Modal ล็อกอิน
    function openLoginModal() {
      document.getElementById('teacher-login-name').value = teacherName !== 'ครูประจำวิชา' ? teacherName : '';
      document.getElementById('teacher-login-room').value = currentRoomCode;
      document.getElementById('login-student-room-code').value = currentRoomCode;
      populateStudentSelects();
      document.getElementById('login-modal').classList.remove('hidden');
    }

    function switchLoginTab(tab) {
      const btnStudent = document.getElementById('btn-tab-student');
      const btnTeacher = document.getElementById('btn-tab-teacher');
      const secStudent = document.getElementById('student-login-section');
      const secTeacher = document.getElementById('teacher-login-section');

      if (tab === 'student') {
        btnStudent.className = 'flex-1 py-2 rounded-xl text-sm font-semibold transition-all bg-white text-indigo-600 shadow-sm';
        btnTeacher.className = 'flex-1 py-2 rounded-xl text-sm font-semibold transition-all text-slate-500 hover:text-slate-800';
        secStudent.classList.remove('hidden');
        secTeacher.classList.add('hidden');
      } else {
        btnTeacher.className = 'flex-1 py-2 rounded-xl text-sm font-semibold transition-all bg-white text-indigo-600 shadow-sm';
        btnStudent.className = 'flex-1 py-2 rounded-xl text-sm font-semibold transition-all text-slate-500 hover:text-slate-800';
        secTeacher.classList.remove('hidden');
        secStudent.classList.add('hidden');
      }
    }

    function populateStudentSelects() {
      const loginSelect = document.getElementById('login-student-select');
      const modalTargetSelect = document.getElementById('modal-student-target');

      if (!studentsData || studentsData.length === 0) {
        if (loginSelect) loginSelect.innerHTML = '<option value="">-- ยังไม่มีรายชื่อในห้องนี้ --</option>';
        if (modalTargetSelect) modalTargetSelect.innerHTML = '<option value="">-- ยังไม่มีนักเรียนในห้อง --</option>';
        return;
      }

      const options = studentsData.map(s => `<option value="${s.id}">${s.name} (ห้อง ${s.room} ${s.number ? 'เลขที่ ' + s.number : ''})</option>`).join('');
      if (loginSelect) loginSelect.innerHTML = options;
      if (modalTargetSelect) modalTargetSelect.innerHTML = options;
    }

    // ครูบันทึกเข้าสู่ระบบ
    function loginAsTeacherSubmit() {
      const nameInput = document.getElementById('teacher-login-name').value.trim();
      const roomInput = document.getElementById('teacher-login-room').value.trim().toUpperCase();

      if (!nameInput || !roomInput) {
        alert('กรุณากรอกชื่อคุณครู และรหัสห้องเรียนให้ครบถ้วน');
        return;
      }

      teacherName = nameInput;
      currentRoomCode = roomInput;
      currentUserRole = 'teacher';
      teacherCurrentView = 'roster';

      saveToLocalStorage();
      updateTeacherDisplay();
      initRealtimeSync();

      document.getElementById('login-modal').classList.add('hidden');
      renderAppView();
    }

    // นักเรียนเข้าใช้ด้วยชื่อเดิม
    function loginAsStudentExisting() {
      const roomInput = document.getElementById('login-student-room-code').value.trim().toUpperCase();
      const select = document.getElementById('login-student-select');

      if (!roomInput) {
        alert('กรุณาระบุรหัสห้องเรียนของคุณครู');
        return;
      }

      if (roomInput !== currentRoomCode) {
        currentRoomCode = roomInput;
        studentsData = [];
        initRealtimeSync();
      }

      if (!select.value) {
        alert('ยังไม่มีรายชื่อในระบบ กรุณากดปุ่ม "นักเรียนใหม่: ลงทะเบียนชื่อตนเอง" ด้านล่าง');
        return;
      }

      currentStudentId = select.value;
      currentUserRole = 'student';

      saveToLocalStorage();
      document.getElementById('login-modal').classList.add('hidden');
      renderAppView();
    }

    function switchTeacherView(view, studentId = null) {
      teacherCurrentView = view;
      if (studentId) {
        currentStudentId = studentId;
        saveToLocalStorage();
      }
      renderAppView();
    }

    // คัดลอกลิงก์ส่งให้นักเรียน
    function copyStudentShareLink() {
      const url = new URL(window.location.href);
      url.searchParams.set('room', currentRoomCode);
      navigator.clipboard.writeText(url.toString()).then(() => {
        alert(`คัดลอกลิงก์ห้องเรียน [${currentRoomCode}] เรียบร้อย!\nส่งให้นักเรียนเข้าห้องนี้ได้ทันที`);
      }).catch(() => {
        prompt('คัดลอกลิงก์นี้ส่งให้นักเรียน:', url.toString());
      });
    }

    // Modal ลงทะเบียนนักเรียน
    function openStudentRegistrationModal(edit = false) {
      isEditingProfile = edit;
      const modal = document.getElementById('register-student-modal');
      const title = document.getElementById('register-modal-title');
      const form = document.getElementById('register-form');
      form.reset();
      tempAvatarBase64 = null;

      const previewImg = document.getElementById('reg-avatar-preview');
      const previewIcon = document.getElementById('reg-avatar-icon');

      if (edit) {
        title.textContent = 'แก้ไขข้อมูลนักเรียน';
        const currentStudent = studentsData.find(s => s.id === currentStudentId);
        if (currentStudent) {
          document.getElementById('reg-name').value = currentStudent.name || '';
          document.getElementById('reg-room').value = currentStudent.room || '';
          document.getElementById('reg-number').value = currentStudent.number || '';
          if (currentStudent.avatar) {
            previewImg.src = currentStudent.avatar;
            previewImg.classList.remove('hidden');
            previewIcon.classList.add('hidden');
            tempAvatarBase64 = currentStudent.avatar;
          } else {
            previewImg.classList.add('hidden');
            previewIcon.classList.remove('hidden');
          }
        }
      } else {
        title.textContent = `ลงทะเบียนนักเรียน (เข้าห้อง ${currentRoomCode})`;
        previewImg.classList.add('hidden');
        previewIcon.classList.remove('hidden');
      }

      document.getElementById('login-modal').classList.add('hidden');
      modal.classList.remove('hidden');
    }

    function closeStudentRegistrationModal() {
      document.getElementById('register-student-modal').classList.add('hidden');
      if (!currentUserRole) openLoginModal();
    }

    // ย่อขนาดรูปภาพก่อนส่งขึ้น Cloud (เพื่อให้ส่งข้อมูลไวปานสายฟ้าแลบ)
    function compressImage(file, callback) {
      const reader = new FileReader();
      reader.onload = function(e) {
        const img = new Image();
        img.onload = function() {
          const canvas = document.createElement('canvas');
          const maxDim = 120;
          let w = img.width;
          let h = img.height;
          if (w > h) {
            if (w > maxDim) { h = Math.round((h * maxDim) / w); w = maxDim; }
          } else {
            if (h > maxDim) { w = Math.round((w * maxDim) / h); h = maxDim; }
          }
          canvas.width = w;
          canvas.height = h;
          const ctx = canvas.getContext('2d');
          ctx.drawImage(img, 0, 0, w, h);
          callback(canvas.toDataURL('image/jpeg', 0.65));
        };
        img.src = e.target.result;
      };
      reader.readAsDataURL(file);
    }

    function previewRegisterAvatar(event) {
      const file = event.target.files[0];
      if (file) {
        compressImage(file, (base64) => {
          tempAvatarBase64 = base64;
          const previewImg = document.getElementById('reg-avatar-preview');
          const previewIcon = document.getElementById('reg-avatar-icon');
          previewImg.src = base64;
          previewImg.classList.remove('hidden');
          previewIcon.classList.add('hidden');
        });
      }
    }

    function handleSaveStudentProfile(e) {
      e.preventDefault();
      const name = document.getElementById('reg-name').value.trim();
      const room = document.getElementById('reg-room').value.trim();
      const number = document.getElementById('reg-number').value.trim();

      if (!name || !room) return;

      let studentObj;

      if (isEditingProfile && currentStudentId) {
        studentObj = studentsData.find(s => s.id === currentStudentId);
        if (studentObj) {
          studentObj.name = name;
          studentObj.room = room;
          studentObj.number = number;
          if (tempAvatarBase64) studentObj.avatar = tempAvatarBase64;
        }
      } else {
        studentObj = {
          id: 'std_' + Date.now(),
          name: name,
          room: room,
          number: number,
          avatar: tempAvatarBase64 || '',
          tasks: []
        };
        studentsData.push(studentObj);
        currentStudentId = studentObj.id;
        if (!currentUserRole) currentUserRole = 'student';
      }

      // บันทึกลง Local และซิงค์ขึ้น Cloud เรียลไทม์ทันที
      saveToLocalStorage();
      broadcastStudent(studentObj);

      document.getElementById('register-student-modal').classList.add('hidden');
      renderAppView();
    }

    function triggerAvatarUpload() {
      if (currentUserRole === 'student' || currentUserRole === 'teacher') {
        document.getElementById('avatar-input').click();
      }
    }

    function changeAvatar(event) {
      const file = event.target.files[0];
      if (file) {
        compressImage(file, (base64) => {
          const student = studentsData.find(s => s.id === currentStudentId);
          if (student) {
            student.avatar = base64;
            saveToLocalStorage();
            broadcastStudent(student);
            renderAppView();
          }
        });
      }
    }

    // แสดงผลหน้าจอหลัก
    function renderAppView() {
      if (!currentUserRole) {
        openLoginModal();
        return;
      }

      updateTeacherDisplay();

      const isTeacher = currentUserRole === 'teacher';
      const teacherBar = document.getElementById('teacher-control-bar');
      const teacherRosterView = document.getElementById('teacher-roster-view');
      const studentDetailWrapper = document.getElementById('student-detail-wrapper');
      const teacherBackBtnBox = document.getElementById('teacher-back-btn-box');
      const userBadge = document.getElementById('user-badge');
      const btnEditProfile = document.getElementById('btn-edit-student-profile');

      document.getElementById('teacher-student-count').textContent = studentsData.length;
      document.getElementById('teacher-student-count-2').textContent = studentsData.length;

      if (isTeacher) {
        teacherBar.classList.remove('hidden');
        btnEditProfile.classList.remove('hidden');
        userBadge.className = 'flex items-center gap-2 px-3 py-1.5 rounded-full text-xs font-semibold bg-purple-100 text-purple-700 border border-purple-200';
        userBadge.innerHTML = `<i class="fa-solid fa-chalkboard-user"></i> ${teacherName}`;

        if (teacherCurrentView === 'roster') {
          teacherRosterView.classList.remove('hidden');
          studentDetailWrapper.classList.add('hidden');
          teacherBackBtnBox.classList.add('hidden');
          renderTeacherStudentRoster();
          return;
        } else {
          teacherRosterView.classList.add('hidden');
          studentDetailWrapper.classList.remove('hidden');
          teacherBackBtnBox.classList.remove('hidden');
        }
      } else {
        teacherBar.classList.add('hidden');
        studentDetailWrapper.classList.remove('hidden');
        teacherBackBtnBox.classList.add('hidden');
        userBadge.className = 'flex items-center gap-2 px-3 py-1.5 rounded-full text-xs font-semibold bg-emerald-100 text-emerald-700 border border-emerald-200';
        userBadge.innerHTML = '<i class="fa-solid fa-user-graduate"></i> นักเรียน';
      }

      const student = studentsData.find(s => s.id === currentStudentId);
      const profileImg = document.getElementById('profile-img');
      const profileIcon = document.getElementById('profile-placeholder-icon');

      if (!student) {
        document.getElementById('display-name').textContent = isTeacher ? 'ยังไม่ได้เลือกนักเรียน' : 'ยังไม่ได้ลงทะเบียน';
        document.getElementById('display-class').textContent = isTeacher ? 'คลิกดูรายชื่อนักเรียนเพื่อเลือก' : 'กรุณากดสลับบทบาทเพื่อลงทะเบียน';
        document.getElementById('role-tag').textContent = isTeacher ? 'โหมดครูผู้สอน' : 'โหมดนักเรียน';
        profileImg.classList.add('hidden');
        profileIcon.classList.remove('hidden');

        updateDashboard({ tasks: [] });
        renderTasks({ tasks: [] }, true);
        return;
      }

      document.getElementById('display-name').textContent = student.name;
      document.getElementById('display-class').textContent = `ห้อง ${student.room} ${student.number ? '• เลขที่ ' + student.number : ''}`;
      document.getElementById('role-tag').textContent = isTeacher ? `กำลังตรวจงานของ: ${student.name}` : 'สมุดติดตามงานของฉัน';

      if (student.avatar) {
        profileImg.src = student.avatar;
        profileImg.classList.remove('hidden');
        profileIcon.classList.add('hidden');
      } else {
        profileImg.classList.add('hidden');
        profileIcon.classList.remove('hidden');
      }

      updateDashboard(student);
      renderTasks(student, false);
    }

    // สร้างการ์ดแสดงผลนักเรียนทุกคนบนหน้าจอคุณครู
    function renderTeacherStudentRoster() {
      const grid = document.getElementById('teacher-students-grid');
      const emptyBox = document.getElementById('teacher-empty-students');

      if (studentsData.length === 0) {
        grid.innerHTML = '';
        emptyBox.classList.remove('hidden');
        emptyBox.classList.add('flex');
        return;
      }

      emptyBox.classList.add('hidden');
      emptyBox.classList.remove('flex');

      grid.innerHTML = studentsData.map(st => {
        const tasks = st.tasks || [];
        const total = tasks.length;
        const pending = tasks.filter(t => !t.completed).length;
        let totalScore = 0;
        let maxScore = 0;
        tasks.forEach(t => {
          if (t.score !== null && t.score !== undefined && t.score !== '') totalScore += parseFloat(t.score);
          if (t.maxScore) maxScore += parseFloat(t.maxScore);
        });

        return `
          <div onclick="switchTeacherView('detail', '${st.id}')" class="group bg-white p-4 rounded-2xl border border-slate-200 hover:border-indigo-400 hover:shadow-lg transition-all cursor-pointer flex flex-col justify-between">
            <div class="flex items-center gap-3">
              <div class="w-12 h-12 rounded-full overflow-hidden bg-indigo-50 flex items-center justify-center flex-shrink-0 text-slate-400 border border-slate-200 group-hover:ring-2 group-hover:ring-indigo-300">
                ${st.avatar ? `<img src="${st.avatar}" class="w-full h-full object-cover">` : '<i class="fa-solid fa-user text-lg"></i>'}
              </div>
              <div class="flex-1 min-w-0">
                <h4 class="font-bold text-slate-800 text-sm truncate group-hover:text-indigo-600 transition-colors">${escapeHtml(st.name)}</h4>
                <p class="text-xs text-slate-400">ห้อง ${escapeHtml(st.room)} ${st.number ? '• เลขที่ ' + escapeHtml(st.number) : ''}</p>
              </div>
            </div>

            <div class="mt-4 pt-3 border-t border-slate-100 grid grid-cols-3 gap-1 text-center">
              <div class="bg-slate-50 py-1.5 rounded-lg">
                <span class="block text-[10px] text-slate-400">งานทั้งหมด</span>
                <span class="text-xs font-bold text-slate-700">${total}</span>
              </div>
              <div class="bg-rose-50 py-1.5 rounded-lg">
                <span class="block text-[10px] text-rose-500">ค้าง</span>
                <span class="text-xs font-bold text-rose-600">${pending}</span>
              </div>
              <div class="bg-amber-50 py-1.5 rounded-lg">
                <span class="block text-[10px] text-amber-500">คะแนน</span>
                <span class="text-xs font-bold text-amber-600">${totalScore}/${maxScore}</span>
              </div>
            </div>

            <div class="mt-3 flex items-center justify-end text-xs text-indigo-500 font-medium group-hover:translate-x-1 transition-transform">
              <span>คลิกตรวจงาน & ให้คะแนน</span> <i class="fa-solid fa-chevron-right ml-1 text-[10px]"></i>
            </div>
          </div>
        `;
      }).join('');
    }

    function updateDashboard(student) {
      const tasks = student.tasks || [];
      const total = tasks.length;
      const completed = tasks.filter(t => t.completed).length;
      const pending = total - completed;

      let currentScore = 0;
      let totalMaxScore = 0;

      tasks.forEach(t => {
        if (t.score !== null && t.score !== undefined && t.score !== '') currentScore += parseFloat(t.score);
        if (t.maxScore) totalMaxScore += parseFloat(t.maxScore);
      });

      document.getElementById('stat-total').textContent = total;
      document.getElementById('stat-pending').textContent = pending;
      document.getElementById('stat-completed').textContent = completed;
      document.getElementById('stat-score').textContent = `${currentScore}/${totalMaxScore}`;
    }

    function renderTasks(student, noStudent = false) {
      const container = document.getElementById('tasks-container');
      const emptyState = document.getElementById('empty-state');
      const emptyTitle = document.getElementById('empty-state-title');
      const emptySub = document.getElementById('empty-state-sub');
      const isTeacher = currentUserRole === 'teacher';

      if (noStudent) {
        container.innerHTML = '';
        emptyState.classList.remove('hidden');
        emptyState.classList.add('flex');
        emptyTitle.textContent = isTeacher ? 'ยังไม่ได้เลือกนักเรียน' : 'ยังไม่ได้ลงทะเบียน';
        emptySub.textContent = isTeacher ? 'กดปุ่มดูรายชื่อนักเรียนเพื่อเลือกคนที่ต้องการตรวจงาน' : 'กรุณากดสลับบทบาทเพื่อกรอกข้อมูลของตนเอง';
        return;
      }

      let filtered = student.tasks || [];
      if (currentFilter === 'pending') filtered = filtered.filter(t => !t.completed);
      else if (currentFilter === 'completed') filtered = filtered.filter(t => t.completed);

      document.getElementById('task-count-label').textContent = `แสดงผล ${filtered.length} รายการ`;

      if (filtered.length === 0) {
        container.innerHTML = '';
        emptyState.classList.remove('hidden');
        emptyState.classList.add('flex');
        emptyTitle.textContent = 'ไม่มีรายการงานในหมวดนี้';
        emptySub.textContent = isTeacher ? 'กดปุ่ม "+ เพิ่มงานให้นักเรียน" เพื่อมอบหมายการบ้าน' : 'ยังไม่มีงานที่คุณครูมอบหมายในหมวดนี้';
        return;
      }

      emptyState.classList.add('hidden');
      emptyState.classList.remove('flex');

      container.innerHTML = filtered.map(task => {
        const isDone = task.completed;
        return `
          <div class="bg-white/90 backdrop-blur-sm border ${isDone ? 'border-emerald-100 bg-emerald-50/20' : 'border-slate-200'} rounded-2xl p-4 shadow-sm hover:shadow-md transition-all flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
            <div class="flex items-start gap-3 flex-1">
              <button ${isTeacher ? `onclick="toggleComplete('${task.id}')"` : 'disabled'} 
                class="mt-1 flex-shrink-0 w-6 h-6 rounded-lg border-2 ${isDone ? 'bg-emerald-500 border-emerald-500 text-white' : 'border-slate-300'} ${isTeacher ? 'cursor-pointer hover:border-indigo-400' : 'cursor-default'} flex items-center justify-center transition-colors">
                ${isDone ? '<i class="fa-solid fa-check text-xs"></i>' : ''}
              </button>
              <div>
                <h4 class="font-semibold text-slate-800 ${isDone ? 'line-through text-slate-400' : ''}">
                  ${escapeHtml(task.title)}
                </h4>
                <div class="flex flex-wrap gap-2 items-center mt-1 text-xs">
                  ${task.subject ? `<span class="px-2 py-0.5 rounded-md bg-indigo-50 text-indigo-600 font-medium">${escapeHtml(task.subject)}</span>` : ''}
                  ${task.deadline ? `<span class="text-slate-400"><i class="fa-regular fa-clock mr-1"></i>ส่ง: ${task.deadline}</span>` : ''}
                  <span class="px-2 py-0.5 rounded-md text-[11px] font-semibold ${isDone ? 'bg-emerald-100 text-emerald-700' : 'bg-rose-100 text-rose-700'}">
                    ${isDone ? 'ส่งแล้ว' : 'ยังไม่ส่ง'}
                  </span>
                </div>
              </div>
            </div>

            <div class="flex items-center justify-between w-full sm:w-auto gap-4 border-t sm:border-t-0 pt-2 sm:pt-0 border-slate-100">
              <div class="text-right">
                ${task.maxScore ? `
                  <div class="text-xs font-semibold ${task.score !== null && task.score !== '' ? 'text-indigo-600' : 'text-slate-400'}">
                    คะแนน: <span class="text-base font-bold">${task.score !== null && task.score !== '' ? task.score : '-'}</span>/${task.maxScore}
                  </div>
                ` : '<span class="text-xs text-slate-300">ไม่มีคะแนน</span>'}
              </div>

              ${isTeacher ? `
                <div class="flex items-center gap-1">
                  <button onclick="openModal('${task.id}')" class="p-2 text-slate-400 hover:text-indigo-500 rounded-lg transition-colors" title="ตรวจคะแนน / แก้ไข">
                    <i class="fa-solid fa-pen text-sm"></i>
                  </button>
                  <button onclick="deleteTask('${task.id}')" class="p-2 text-slate-400 hover:text-rose-500 rounded-lg transition-colors" title="ลบงาน">
                    <i class="fa-solid fa-trash-can text-sm"></i>
                  </button>
                </div>
              ` : ''}
            </div>
          </div>
        `;
      }).join('');
    }

    function filterTasks(filter) {
      currentFilter = filter;
      const tabs = ['all', 'pending', 'completed'];
      tabs.forEach(tab => {
        const btn = document.getElementById(`tab-${tab}`);
        if (tab === filter) {
          btn.className = 'px-3 sm:px-4 py-1.5 rounded-xl bg-white text-indigo-600 shadow-sm transition-all font-medium';
        } else {
          btn.className = 'px-3 sm:px-4 py-1.5 rounded-xl text-slate-600 hover:text-slate-900 transition-all';
        }
      });
      const student = studentsData.find(s => s.id === currentStudentId);
      renderTasks(student || { tasks: [] }, !student);
    }

    // ครูตรวจติ๊กสถานะเสร็จ/ค้าง
    function toggleComplete(taskId) {
      if (currentUserRole !== 'teacher') return;
      const student = studentsData.find(s => s.id === currentStudentId);
      if (!student) return;
      const task = student.tasks.find(t => t.id === taskId);
      if (task) {
        task.completed = !task.completed;
        saveToLocalStorage();
        broadcastStudent(student);
        renderAppView();
      }
    }

    function deleteTask(taskId) {
      if (currentUserRole !== 'teacher') return;
      if (confirm('คุณครูต้องการลบงานนี้ใช่หรือไม่?')) {
        const student = studentsData.find(s => s.id === currentStudentId);
        if (student) {
          student.tasks = student.tasks.filter(t => t.id !== taskId);
          saveToLocalStorage();
          broadcastStudent(student);
          renderAppView();
        }
      }
    }

    // Modal จัดการงาน
    function openModal(taskId = null) {
      if (currentUserRole !== 'teacher') return;
      if (studentsData.length === 0) {
        alert('ยังไม่มีนักเรียนในห้องเรียนนี้ กรุณารอนักเรียนลงทะเบียน หรือกด "ครูช่วยเพิ่มนักเรียน" ก่อนสั่งงาน');
        return;
      }

      populateStudentSelects();
      const modal = document.getElementById('task-modal');
      const form = document.getElementById('task-form');
      const assignBox = document.getElementById('modal-assign-student-box');
      const studentTarget = document.getElementById('modal-student-target');
      form.reset();

      if (taskId) {
        assignBox.classList.add('hidden');
        const student = studentsData.find(s => s.id === currentStudentId);
        const task = student?.tasks.find(t => t.id === taskId);
        if (task) {
          document.getElementById('modal-title').textContent = 'แก้ไขงาน / ตรวจให้คะแนน';
          document.getElementById('task-id').value = task.id;
          document.getElementById('task-title').value = task.title;
          document.getElementById('task-subject').value = task.subject || '';
          document.getElementById('task-deadline').value = task.deadline || '';
          document.getElementById('task-max-score').value = task.maxScore || '';
          document.getElementById('task-score').value = task.score !== null ? task.score : '';
          document.getElementById('task-completed-checkbox').checked = !!task.completed;
        }
      } else {
        document.getElementById('modal-title').textContent = 'มอบหมายงานใหม่ให้นักเรียน';
        document.getElementById('task-id').value = '';
        document.getElementById('task-completed-checkbox').checked = false;
        if (currentStudentId) studentTarget.value = currentStudentId;
        assignBox.classList.remove('hidden');
      }

      modal.classList.remove('hidden');
    }

    function closeModal() {
      document.getElementById('task-modal').classList.add('hidden');
    }

    function saveTask(e) {
      e.preventDefault();
      if (currentUserRole !== 'teacher') return;

      const id = document.getElementById('task-id').value;
      const targetStudentId = id ? currentStudentId : document.getElementById('modal-student-target').value;
      const student = studentsData.find(s => s.id === targetStudentId);
      if (!student) return;

      const title = document.getElementById('task-title').value.trim();
      const subject = document.getElementById('task-subject').value.trim();
      const deadline = document.getElementById('task-deadline').value;
      const maxScore = document.getElementById('task-max-score').value;
      const score = document.getElementById('task-score').value;
      const completed = document.getElementById('task-completed-checkbox').checked;

      if (!title) return;

      if (id) {
        const task = student.tasks.find(t => t.id === id);
        if (task) {
          task.title = title;
          task.subject = subject;
          task.deadline = deadline;
          task.maxScore = maxScore ? parseFloat(maxScore) : null;
          task.score = score !== '' ? parseFloat(score) : null;
          task.completed = completed;
        }
      } else {
        if (!student.tasks) student.tasks = [];
        student.tasks.unshift({
          id: Date.now().toString(),
          title: title,
          subject: subject,
          deadline: deadline,
          maxScore: maxScore ? parseFloat(maxScore) : null,
          score: score !== '' ? parseFloat(score) : null,
          completed: completed
        });
        currentStudentId = student.id;
        teacherCurrentView = 'detail';
      }

      saveToLocalStorage();
      broadcastStudent(student);
      closeModal();
      renderAppView();
    }

    function escapeHtml(text) {
      if (!text) return '';
      return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
    }

    // เริ่มการทำงานระบบทันที
    updateTeacherDisplay();
    initRealtimeSync();
    renderAppView();
  </script>
</body>
</html>
