<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal Laporan - PT. Sinar Randu Indah</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        .fade-in { animation: fadeIn 0.3s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        #toast { animation: slideUp 2.5s ease-in-out forwards; }
        @keyframes slideUp { 0%, 100% { opacity: 0; transform: translate(-50%, 20px); } 15%, 85% { opacity: 1; transform: translate(-50%, 0); } }
    </style>
</head>
<body class="bg-[#f4f7f5] min-h-screen py-6 px-4 md:py-12 flex flex-col items-center justify-center">

    <!-- MENU UTAMA -->
    <div id="view-menu" class="w-full max-w-lg bg-white rounded-2xl shadow-md border border-emerald-100/60 overflow-hidden fade-in">
        <div class="bg-gradient-to-r from-emerald-600 to-teal-600 p-8 text-center text-white">
            <h1 class="text-2xl font-bold tracking-tight mb-1">Portal Pelaporan</h1>
            <p class="text-sm font-medium text-emerald-100">PT. Sinar Randu Indah</p>
        </div>
        <div class="p-6 space-y-4">
            <button onclick="showView('view-antrian')" class="w-full bg-slate-50 hover:bg-emerald-50 border border-slate-200 hover:border-emerald-300 transition-all p-5 rounded-xl flex items-center group text-left">
                <div class="bg-emerald-100 text-emerald-700 w-12 h-12 rounded-full flex items-center justify-center flex-shrink-0 group-hover:scale-110 transition-transform">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17a2 2 0 11-4 0 2 2 0 014 0zM19 17a2 2 0 11-4 0 2 2 0 014 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16V6a1 1 0 00-1-1H4a1 1 0 00-1 1v10a1 1 0 001 1h1m8-1a1 1 0 01-1 1H9m4-1V8a1 1 0 011-1h2.586a1 1 0 01.707.293l3.414 3.414a1 1 0 01.293.707V16a1 1 0 01-1 1h-1m-6-1a1 1 0 001 1h1M5 17a2 2 0 104 0m-4 0a2 2 0 114 0m6 0a2 2 0 104 0m-4 0a2 2 0 114 0"></path></svg>
                </div>
                <div class="ml-4">
                    <h2 class="text-lg font-bold text-slate-800">Laporan Antrian TBS</h2>
                    <p class="text-xs text-slate-500">Rekap data jumlah kendaraan.</p>
                </div>
            </button>

            <button onclick="showView('view-segel')" class="w-full bg-slate-50 hover:bg-teal-50 border border-slate-200 hover:border-teal-300 transition-all p-5 rounded-xl flex items-center group text-left">
                <div class="bg-teal-100 text-teal-700 w-12 h-12 rounded-full flex items-center justify-center flex-shrink-0 group-hover:scale-110 transition-transform">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z"></path></svg>
                </div>
                <div class="ml-4">
                    <h2 class="text-lg font-bold text-slate-800">Laporan Segel</h2>
                    <p class="text-xs text-slate-500">Nopol, Driver, No Segel, dll.</p>
                </div>
            </button>
        </div>
    </div>

    <!-- VIEW ANTRIAN -->
    <div id="view-antrian" class="hidden w-full max-w-lg bg-white rounded-2xl shadow-md border border-emerald-100/60 overflow-hidden fade-in">
        <div class="bg-gradient-to-r from-emerald-50/80 to-teal-50/50 p-4 border-b border-emerald-100/50 relative">
            <button onclick="showView('view-menu')" class="absolute top-4 left-4 text-emerald-700 hover:text-emerald-900 flex items-center text-xs font-bold px-2 py-1 bg-white rounded-md border border-emerald-200 shadow-sm transition-all active:scale-95">← Ke Menu</button>
            <div class="mt-8 text-center"><h1 class="text-xl font-bold text-emerald-900">Laporan Antrian TBS</h1></div>
        </div>
        <div class="p-6 space-y-4">
            <div class="grid grid-cols-2 gap-4">
                <div><label class="text-[10px] text-slate-400 font-bold uppercase">Tanggal</label><input type="date" id="tanggal" class="w-full border rounded-lg p-2 text-sm" onchange="generateLaporanAntrian()"></div>
                <div><label class="text-[10px] text-slate-400 font-bold uppercase">Jam</label><input type="time" id="jam" class="w-full border rounded-lg p-2 text-sm" onchange="generateLaporanAntrian()"></div>
            </div>
            <div class="space-y-3">
                <div class="flex justify-between items-center text-sm"><span>Fuso</span><input type="number" id="fuso" value="0" class="w-20 border rounded p-1 text-right" oninput="generateLaporanAntrian()"></div>
                <div class="flex justify-between items-center text-sm"><span>CD DT</span><input type="number" id="cddt" value="0" class="w-20 border rounded p-1 text-right" oninput="generateLaporanAntrian()"></div>
                <div class="flex justify-between items-center text-sm"><span>CD</span><input type="number" id="cd" value="0" class="w-20 border rounded p-1 text-right" oninput="generateLaporanAntrian()"></div>
                <div class="flex justify-between items-center text-sm"><span>Pick Up</span><input type="number" id="pickup" value="0" class="w-20 border rounded p-1 text-right" oninput="generateLaporanAntrian()"></div>
                <div class="flex justify-between items-center text-sm font-bold text-emerald-700"><span>Sudah Bongkar</span><input type="number" id="bongkar" value="0" class="w-20 border rounded p-1 text-right" oninput="generateLaporanAntrian()"></div>
            </div>
            <div class="text-center font-bold text-lg pt-2 border-t">Total Terparkir: <span id="total-display">0</span></div>
            <textarea id="preview-antrian" class="hidden"></textarea>
            <button onclick="salinTeks('preview-antrian')" class="w-full bg-emerald-700 text-white py-3 rounded-xl font-bold">Salin Laporan WhatsApp</button>
        </div>
    </div>

    <!-- VIEW SEGEL -->
    <div id="view-segel" class="hidden w-full max-w-lg bg-white rounded-2xl shadow-md border border-teal-100/60 overflow-hidden fade-in">
        <div class="bg-gradient-to-r from-teal-50/80 to-blue-50/50 p-4 border-b border-teal-100/50 relative">
            <button onclick="showView('view-menu')" class="absolute top-4 left-4 text-teal-700 hover:text-teal-900 flex items-center text-xs font-bold px-2 py-1 bg-white rounded-md border border-teal-200 shadow-sm transition-all active:scale-95">← Ke Menu</button>
            <div class="mt-8 text-center"><h1 class="text-xl font-bold text-teal-900">Laporan Segel</h1></div>
        </div>
        <div class="p-6 space-y-4">
            <div><label class="text-[10px] font-bold text-slate-500 uppercase">Data Driver</label><input type="text" id="segel-nopol" placeholder="MASUKKAN NOPOL" class="w-full border p-2 rounded-lg text-sm mb-1 uppercase" oninput="generateLaporanSegel()"><input type="text" id="segel-driver" placeholder="MASUKKAN NAMA DRIVER" class="w-full border p-2 rounded-lg text-sm uppercase" oninput="generateLaporanSegel()"></div>
            <div>
                <label class="text-[10px] font-bold text-slate-500 uppercase">Auto Generate Segel</label>
                <div class="flex gap-2 mb-2">
                    <input type="text" id="segel-awal" placeholder="No Awal (Cth: 0005031)" class="w-full border p-2 rounded-lg text-sm">
                    <input type="number" id="segel-jumlah-input" placeholder="Jml" class="w-16 border p-2 rounded-lg text-sm text-center">
                    <button onclick="generateUrutanSegel()" class="bg-teal-600 text-white px-3 py-2 rounded-lg text-xs font-bold">BUAT</button>
                </div>
                <textarea id="segel-list" rows="3" class="w-full border p-2 rounded-lg text-sm uppercase" placeholder="LIST NOMOR SEGEL (PISAHKAN DENGAN KOMA)" oninput="generateLaporanSegel()"></textarea>
            </div>
            <div><label class="text-[10px] font-bold text-slate-500 uppercase">Muatan & Tujuan</label><input type="text" id="segel-muatan" value="CPO" class="w-full border p-2 rounded-lg text-sm mb-1 uppercase" oninput="generateLaporanSegel()"><input type="text" id="segel-tujuan" value="PT. TBL" class="w-full border p-2 rounded-lg text-sm uppercase" oninput="generateLaporanSegel()"></div>
            <textarea id="preview-segel" class="hidden"></textarea>
            <button onclick="salinTeks('preview-segel')" class="w-full bg-teal-600 text-white py-3 rounded-xl font-bold hover:bg-teal-700">Salin Laporan WhatsApp</button>
        </div>
    </div>

    <div class="text-center text-[10px] text-slate-400 mt-6 font-bold uppercase tracking-widest">Dibuat oleh. Komang Arya Budana</div>
    <div id="toast" class="hidden fixed bottom-10 left-1/2 transform -translate-x-1/2 bg-slate-900/90 text-white px-5 py-3 rounded-full shadow-lg z-50 text-xs font-bold items-center border border-slate-800">BERHASIL DISALIN!</div>

    <script>
        function showView(id) {
            document.getElementById('view-menu').classList.add('hidden');
            document.getElementById('view-antrian').classList.add('hidden');
            document.getElementById('view-segel').classList.add('hidden');
            document.getElementById(id).classList.remove('hidden');
        }

        function generateLaporanAntrian() {
            const f = parseInt(document.getElementById('fuso').value) || 0;
            const c = parseInt(document.getElementById('cddt').value) || 0;
            const cd = parseInt(document.getElementById('cd').value) || 0;
            const p = parseInt(document.getElementById('pickup').value) || 0;
            const b = parseInt(document.getElementById('bongkar').value) || 0;
            const total = f + c + cd + p;
            document.getElementById('total-display').innerText = total;
            document.getElementById('preview-antrian').value = `*LAPORAN JUMLAH KENDARAAN ANTRI TBS*\n*AREA PARKIR PT. SRI*\n\nHARI, ${document.getElementById('tanggal').value}\nPUKUL  : ${document.getElementById('jam').value} WIB\n\nRINCIAN KENDARAAN :\n\nFUSO : ${f} UNIT\nCD DT  : ${c} UNIT\nCD  : ${cd} UNIT\nPICK UP  : ${p} UNIT \n\nJUMLAH TERPARKIR  : ${total} UNIT\nSUDAH BONGKAR     : ${b} UNIT`.toUpperCase();
        }

        function generateUrutanSegel() {
            const awal = document.getElementById('segel-awal').value.trim();
            const jml = parseInt(document.getElementById('segel-jumlah-input').value) || 0;
            const match = awal.match(/^(\D*)(\d+)(\D*)$/);
            if (match && jml > 0) {
                let list = [];
                let start = parseInt(match[2]);
                for(let i=0; i<jml; i++) list.push(match[1] + (start+i).toString().padStart(match[2].length, '0') + match[3]);
                document.getElementById('segel-list').value = list.join(', ');
                generateLaporanSegel();
            }
        }

        function generateLaporanSegel() {
            const list = document.getElementById('segel-list').value;
            const arr = list.split(',').filter(s => s.trim() !== '');
            const txt = `NOPOL : ${document.getElementById('segel-nopol').value}\nDRIVER : ${document.getElementById('segel-driver').value}\n\nNO SEGEL : ${list}\n\nJUMLAH SEGEL : ${arr.length}\nJENIS MUATAN : ${document.getElementById('segel-muatan').value}\nTUJUAN : ${document.getElementById('segel-tujuan').value}`.toUpperCase();
            document.getElementById('preview-segel').value = txt;
        }

        function salinTeks(id) {
            const el = document.getElementById(id);
            el.style.display = 'block';
            el.select();
            document.execCommand("copy");
            el.style.display = 'none';
            const toast = document.getElementById("toast");
            toast.classList.remove("hidden");
            setTimeout(() => toast.classList.add("hidden"), 2000);
        }
    </script>
</body>
</html>