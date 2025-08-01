<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Profil Saya - [Nama Lengkap Anda]</title>

    <script src="https://kit.fontawesome.com/YOUR_FONT_AWESOME_KIT_ID.js" crossorigin="anonymous"></script>

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

    <style>
        :root {
            --primary-color: #4CAF50; /* Hijau yang menyegarkan */
            --secondary-color: #2196F3; /* Biru cerah */
            --accent-color: #FFC107; /* Kuning cerah */
            --text-color: #333;
            --bg-light: #f4f7f6;
            --bg-dark: #e0e6e4;
            --border-radius: 8px;
            --shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Poppins', sans-serif;
            line-height: 1.6;
            color: var(--text-color);
            background-color: var(--bg-light);
            padding-top: 60px; /* Ruang untuk header tetap */
        }

        /* Header */
        header {
            background-color: #fff;
            color: var(--text-color);
            padding: 20px 0;
            text-align: center;
            box-shadow: var(--shadow);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
        }

        .profile-pic-container {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            overflow: hidden;
            margin: 0 auto 15px;
            border: 4px solid var(--primary-color);
            box-shadow: 0 0 0 5px rgba(76, 175, 80, 0.3);
        }

        .profile-pic {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }

        header h1 {
            font-size: 2.5em;
            margin-bottom: 5px;
            color: var(--primary-color);
        }

        header .tagline {
            font-size: 1.1em;
            color: #666;
            margin-bottom: 15px;
        }

        /* Tombol Toggle Profil */
        #toggleProfileBtn {
            background-color: var(--secondary-color);
            color: #fff;
            padding: 10px 20px;
            border: none;
            border-radius: var(--border-radius);
            cursor: pointer;
            font-size: 1em;
            transition: background-color 0.3s ease, transform 0.2s ease;
            margin-top: 10px;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        #toggleProfileBtn:hover {
            background-color: #1976d2;
            transform: translateY(-2px);
        }

        /* Kontainer Profil yang Dapat Disembunyikan */
        #profileContent {
            max-height: 500px; /* Tinggi maksimum awal yang cukup besar */
            opacity: 1;
            overflow: hidden;
            transition: max-height 0.7s ease-in-out, opacity 0.5s ease-out;
            will-change: max-height, opacity;
        }

        #profileContent.hidden {
            max-height: 0;
            opacity: 0;
            padding-top: 0;
            padding-bottom: 0;
            margin-bottom: 0;
        }

        /* Navigasi */
        nav {
            background-color: var(--primary-color);
            box-shadow: var(--shadow);
            text-align: center;
            position: sticky;
            top: 156px; /* Akan disesuaikan oleh JavaScript */
            z-index: 999;
        }

        nav ul {
            list-style: none;
            display: flex;
            justify-content: center;
            padding: 10px 0;
        }

        nav ul li {
            margin: 0 15px;
        }

        nav ul li a {
            color: #fff;
            text-decoration: none;
            font-weight: 600;
            padding: 8px 15px;
            transition: background-color 0.3s ease, border-radius 0.3s ease;
            border-radius: var(--border-radius);
        }

        nav ul li a:hover,
        nav ul li a.active {
            background-color: rgba(255, 255, 255, 0.2);
            border-radius: var(--border-radius);
        }

        /* Konten Utama */
        main {
            max-width: 900px;
            margin: 30px auto;
            padding: 0 20px;
        }

        /* Gaya Umum untuk Setiap Bagian (Section) */
        section {
            background-color: #fff;
            padding: 30px;
            margin-bottom: 25px;
            border-radius: var(--border-radius);
            box-shadow: var(--shadow);
            opacity: 0; /* Untuk animasi fade-in */
            transform: translateY(20px); /* Untuk animasi fade-in */
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }

        section.fade-in {
            opacity: 1;
            transform: translateY(0);
        }

        /* Judul H2 di Setiap Bagian */
        section h2 {
            color: var(--primary-color);
            font-size: 2em;
            margin-bottom: 20px;
            text-align: center;
            position: relative;
            padding-bottom: 10px;
        }

        section h2::after {
            content: '';
            position: absolute;
            left: 50%;
            bottom: 0;
            transform: translateX(-50%);
            width: 60px;
            height: 3px;
            background-color: var(--accent-color);
            border-radius: 5px;
        }

        section p {
            margin-bottom: 15px;
            line-height: 1.8;
        }

        /* Bagian Hobi */
        .hobbies-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .hobby-item {
            background-color: var(--bg-light);
            padding: 20px;
            border-radius: var(--border-radius);
            text-align: center;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s ease;
        }

        .hobby-item:hover {
            transform: translateY(-5px);
        }

        .hobby-item h3 {
            color: var(--secondary-color);
            margin-bottom: 10px;
            font-size: 1.3em;
        }

        .hobby-item i {
            font-size: 2em;
            color: var(--accent-color);
            margin-bottom: 10px;
        }

        /* Riwayat Pendidikan (Timeline) */
        .timeline {
            position: relative;
            padding: 20px 0;
            margin-top: 20px;
        }

        .timeline::before {
            content: '';
            position: absolute;
            left: 50%;
            top: 0;
            width: 4px;
            height: 100%;
            background: var(--bg-dark);
            transform: translateX(-50%);
        }

        .timeline-item {
            width: 50%;
            padding: 10px 40px;
            position: relative;
            background-color: #fff;
            border-radius: var(--border-radius);
            margin-bottom: 20px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s ease;
        }

        .timeline-item:hover {
            transform: translateY(-5px);
        }

        .timeline-item:nth-child(odd) {
            left: 0;
            text-align: right;
        }

        .timeline-item:nth-child(even) {
            left: 50%;
        }

        .timeline-item::after {
            content: '';
            position: absolute;
            width: 15px;
            height: 15px;
            background-color: var(--primary-color);
            border: 3px solid var(--accent-color);
            border-radius: 50%;
            top: 20px;
            z-index: 1;
        }

        .timeline-item:nth-child(odd)::after {
            right: -7.5px;
        }

        .timeline-item:nth-child(even)::after {
            left: -7.5px;
        }

        .timeline-item h3 {
            color: var(--primary-color);
            margin-bottom: 5px;
        }

        .timeline-item .timeline-date {
            font-size: 0.9em;
            color: #888;
            margin-bottom: 10px;
            display: block;
        }

        /* Keterampilan */
        .skills-category {
            margin-bottom: 25px;
        }

        .skills-category h3 {
            color: var(--secondary-color);
            margin-bottom: 15px;
            font-size: 1.4em;
            border-bottom: 2px solid var(--bg-dark);
            padding-bottom: 5px;
        }

        .skill-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .skill-tags span {
            background-color: var(--primary-color);
            color: #fff;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9em;
            font-weight: 500;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            transition: background-color 0.3s ease;
        }

        .skill-tags span:hover {
            background-color: #388e3c;
        }

        /* Kontak */
        .contact-links {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
        }

        .contact-button {
            background-color: var(--secondary-color);
            color: #fff;
            padding: 12px 25px;
            border-radius: var(--border-radius);
            text-decoration: none;
            font-weight: 600;
            transition: background-color 0.3s ease, transform 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .contact-button:hover {
            background-color: #1976d2;
            transform: translateY(-3px);
        }

        .contact-button i {
            font-size: 1.2em;
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 20px;
            margin-top: 40px;
            background-color: var(--primary-color);
            color: #fff;
            font-size: 0.9em;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        /* Responsivitas */
        @media (max-width: 768px) {
            header h1 {
                font-size: 2em;
            }

            nav ul {
                flex-direction: column;
                padding: 10px;
            }

            nav ul li {
                margin: 5px 0;
            }

            .timeline::before {
                left: 20px;
            }

            .timeline-item {
                width: 100%;
                padding: 10px 20px 10px 60px;
                left: 0 !important;
                text-align: left !important;
            }

            .timeline-item::after {
                left: 13px !important;
            }

            .hobbies-grid {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 480px) {
            section {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <header>
        <div id="profileContent">
            <div class="profile-pic-container">
                <img src="C:\Users\ZYREX\Pictures\9bac497f-b18d-4075-b07f-0f70b1c0c5a2.jfif" alt="Foto Profil Anda" class="profile-pic">
            </div>
            <h1>Halo, Saya Lutfi Telapary!</h1>
            <p class="tagline">Selamat Datang Di Profil Saya</p>
        </div>
        <button id="toggleProfileBtn">
            <i class="fas fa-eye-slash"></i> <span>Sembunyikan Profil</span>
        </button>
    </header>

    <nav>
        <ul>
            <li><a href="#about">Tentang Saya</a></li>
            <li><a href="#hobbies">Hobi</a></li>
            <li><a href="#education">Pendidikan</a></li>
            <li><a href="#skills">Keterampilan</a></li>
            <li><a href="#contact">Kontak</a></li>
        </ul>
    </nav>

    <main>
        <section id="about" class="fade-in">
            <h2>Tentang Saya</h2>
            <p>Halo! Perkenalkan nama saya Lutfi Telapary, saya seorang mahasiswa Universitas Kristen Indonesia Maluku yang berada pada semester 4 di Fakultas Ilmu Komputer, Program Studi Informatika.</p>
            <p>Saya berumur 19 Tahun.</p>
			<p>Saya berasal dari Rutong.</p>
        </section>

        <section id="hobbies" class="fade-in">
            <h2>Hobi & Minat</h2>
            <div class="hobbies-grid">
                <div class="hobby-item">
                    <h3><i class="fas fa-gadget"></i> Bermain Game</h3>
                    <p>Saya suka bermain game online maupun offline, game yang saya mainkan ialah: PUBG, Football, Biliard.</p>
                </div>
                <div class="hobby-item">
                    <h3><i class="fas fa-music"></i> Mendengarkan Musik</h3>
                    <p>Musik adalah sumber inspirasi dan relaksasi saya. Saya suka mendengarkan musik disaat lagi berkendara ataupun lagi tidak berbuat apa-apa.</p>
                </div>
                <div class="hobby-item">
                    <h3><i class="fas fa-dance"></i> Dancer</h3>
                    <p>Saya suka sekali dengan Dance, Banyak sekali dance-dance di Titok yang saya Lihat untuk dipelajari dan dipraktekan.</p>
                </div>
                </div>
        </section>

        <section id="education" class="fade-in">
            <h2>Riwayat Pendidikan</h2>
            <div class="timeline">
                <div class="timeline-item">
                    <h3>Universitas Kristen Indonesia Maluku</h3>
                    <p class="timeline-date">[Tahun Masuk 2023] - [Tahun Lulus]</p>
                    <p><strong>Fakultas Ilmu Komputer/Program Studi Informatika</strong></p>
                </div>
                <div class="timeline-item">
                    <h3>Sekolah Menengah Atas (SMK Negeri 6 Ambon)</h3>
                    <p class="timeline-date">[Tahun Masuk 2019] - [Tahun Lulus 2023]</p>
                    <p><strong>Jurusan Multimedia</strong></p>
                </div>
				<div class="timeline-item">
                    <h3>Sekolah Menengah Pertama (SMP Negeri 6 Ambon)</h3>
                    <p class="timeline-date">[Tahun Masuk 2017] - [Tahun Lulus 2029]</p>
                </div>
				<div class="timeline-item">
                    <h3>Sekolah Dasar (SD Negeri 6 Ambon)</h3>
                    <p class="timeline-date">[Tahun Masuk 2011] - [Tahun Lulus 2017]</p>
        </section>

        <section id="skills" class="fade-in">
            <h2>Keterampilan Saya</h2>
            <div class="skills-category">
                <h3>Bahasa Pemrograman</h3>
                <div class="skill-tags">
                    <span>HTML5</span>
                    <span>CSS3</span>
                    <span>JavaScript</span>
                    </div>
            </div>
            <div class="skills-category">
                <h3>Multimedia</h3>
                <div class="skill-tags">
                    <span>Capcut</span>
                    <span>Figma</span>
                    <span>Adobe Photoshop</span>
                    </div>
            </div>
        </section>

        <section id="contact" class="fade-in">
            <h2>Hubungi Saya Jika Anda Butuhkan!</h2>
            <div class="contact-links">
                <a href="https://www.instagram.com/upitelapary_?igsh=MXBtYWw5ZjNobHdocA==" target="_blank" class="contact-button"><i class="fab fa-instagram"></i> Instagram</a>
            </div>
        </section>
    </main>

    <footer>
        <p>&copy; 2025 LutfiTelapary.</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // --- Fungsi Toggle Profil ---
            const toggleProfileBtn = document.getElementById('toggleProfileBtn');
            const profileContent = document.getElementById('profileContent');
            const navBar = document.querySelector('nav');
            const toggleIcon = toggleProfileBtn.querySelector('i'); // Ikon di dalam tombol
            const toggleText = toggleProfileBtn.querySelector('span'); // Teks di dalam tombol

            // Fungsi untuk menghitung ulang posisi sticky nav
            function updateNavStickyPosition() {
                const headerHeight = document.querySelector('header').offsetHeight;
                navBar.style.top = headerHeight + 'px';
            }

            // Panggil saat halaman dimuat untuk pengaturan awal
            updateNavStickyPosition();


            toggleProfileBtn.addEventListener('click', function() {
                profileContent.classList.toggle('hidden');

                // Ubah ikon dan teks tombol sesuai status
                if (profileContent.classList.contains('hidden')) {
                    toggleIcon.classList.remove('fa-eye-slash');
                    toggleIcon.classList.add('fa-eye');
                    toggleText.textContent = 'Tampilkan Profil';
                } else {
                    toggleIcon.classList.remove('fa-eye');
                    toggleIcon.classList.add('fa-eye-slash');
                    toggleText.textContent = 'Sembunyikan Profil';
                }

                // Perbarui posisi navigasi setelah toggle (dengan sedikit delay untuk animasi)
                // Delay disesuaikan dengan transisi CSS max-height (0.7s)
                setTimeout(updateNavStickyPosition, 700);
            });

            // --- Fungsionalitas Navigasi dan Animasi Scroll ---

            // Smooth scrolling untuk navigasi
            document.querySelectorAll('nav a').forEach(anchor => {
                anchor.addEventListener('click', function(e) {
                    e.preventDefault();

                    const targetId = this.getAttribute('href').substring(1);
                    const targetSection = document.getElementById(targetId);

                    if (targetSection) {
                        const headerOffset = document.querySelector('header').offsetHeight;
                        const navOffset = document.querySelector('nav').offsetHeight;
                        const totalOffset = headerOffset + navOffset + 20; // 20px padding ekstra

                        window.scrollTo({
                            top: targetSection.offsetTop - totalOffset,
                            behavior: 'smooth'
                        });
                    }

                    // Hapus kelas 'active' dari semua tautan navigasi
                    document.querySelectorAll('nav a').forEach(link => {
                        link.classList.remove('active');
                    });
                    // Tambahkan kelas 'active' ke tautan yang diklik
                    this.classList.add('active');
                });
            });

            // Animasi fade-in saat scroll menggunakan Intersection Observer
            const sections = document.querySelectorAll('section');
            const observerOptions = {
                root: null,
                rootMargin: '0px',
                threshold: 0.2 // Ketika 20% dari bagian terlihat
            };

            const observer = new IntersectionObserver((entries, observer) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('fade-in');
                        // observer.unobserve(entry.target); // Opsional: hentikan observasi setelah animasi pertama
                    }
                });
            }, observerOptions);

            sections.forEach(section => {
                observer.observe(section);
            });

            // Atur tautan navigasi 'active' saat memuat halaman atau scroll
            function setActiveNavLink() {
                const headerOffset = document.querySelector('header').offsetHeight;
                const navOffset = document.querySelector('nav').offsetHeight;
                const totalOffset = headerOffset + navOffset + 20;

                let currentActiveSectionId = null;

                sections.forEach(section => {
                    const sectionTop = section.offsetTop - totalOffset;
                    const sectionBottom = sectionTop + section.offsetHeight;

                    if (window.scrollY >= sectionTop && window.scrollY < sectionBottom) {
                        currentActiveSectionId = section.id;
                    }
                });

                document.querySelectorAll('nav a').forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href').substring(1) === currentActiveSectionId) {
                        link.classList.add('active');
                    }
                });
            }

            window.addEventListener('load', setActiveNavLink);
            window.addEventListener('scroll', setActiveNavLink);

            // Panggilan awal untuk memastikan tautan navigasi yang benar aktif
            setActiveNavLink();
        });
    </script>
</body>
</html>
