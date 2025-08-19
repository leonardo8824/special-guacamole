<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TDD - Veículos Personalizados</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary: #b32121;
            --secondary: #292f35;
            --light: #ecf0f1;
            --dark: #1a1a1a;
            --accent: #e67e22;
        }
        
        body {
            background-color: #f5f5f5;
            color: #353333;
            line-height: 1.6;
            overflow-x: hidden;
        }
        
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 15px;
        }
        
        /* Header */
        header {
            background-color: var(--secondary);
            color: rgb(255, 243, 243);
            padding: 15px 0;
            position: sticky;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .logo h1 {
            font-size: 1.8rem;
            font-weight: 700;
        }
        
        .logo span {
            color: var(--primary);
        }
        
        nav ul {
            display: flex;
            list-style: none;
            gap: 30px;
        }
        
        nav a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            font-size: 1.1rem;
            transition: color 0.3s;
            position: relative;
            padding: 5px 0;
        }
        
        nav a:hover {
            color: var(--primary);
        }
        
        nav a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background-color: var(--primary);
            transition: width 0.3s;
        }
        
        nav a:hover::after {
            width: 100%;
        }
        
        .mobile-menu {
            display: none;
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        /* Hero Section */
        .hero {
            background: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)), url('https://images.unsplash.com/photo-1544829099-b9a0c07fad1a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2000&q=80');
            background-size: cover;
            background-position: center;
            height: 90vh;
            display: flex;
            align-items: center;
            text-align: center;
            color: white;
            position: relative;
        }
        
        .hero-content {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            animation: fadeInUp 1s ease;
        }
        
        .hero h1 {
            font-size: 3.5rem;
            margin-bottom: 20px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }
        
        .hero p {
            font-size: 1.5rem;
            margin-bottom: 40px;
        }
        
        .btn {
            display: inline-block;
            background-color: var(--primary);
            color: white;
            padding: 15px 40px;
            border-radius: 30px;
            text-decoration: none;
            font-weight: bold;
            font-size: 1.1rem;
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 1px;
            border: 2px solid var(--primary);
        }
        
        .btn:hover {
            background-color: transparent;
            color: var(--primary);
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        /* Services Section */
        .services {
            padding: 100px 0;
            background-color: white;
        }
        
        .section-title {
            text-align: center;
            margin-bottom: 60px;
        }
        
        .section-title h2 {
            font-size: 2.5rem;
            color: var(--secondary);
            margin-bottom: 15px;
            position: relative;
            display: inline-block;
        }
        
        .section-title h2::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background-color: var(--primary);
        }
        
        .section-title p {
            color: #d3cece;
            max-width: 700px;
            margin: 20px auto 0;
            font-size: 1.1rem;
        }
        
        .services-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
        }
        
        .service-card {
            background-color: var(--light);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            transition: all 0.4s;
        }
        
        .service-card:hover {
            transform: translateY(-15px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
        }
        
        .service-img {
            height: 250px;
            overflow: hidden;
        }
        
        .service-img img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s;
        }
        
        .service-card:hover .service-img img {
            transform: scale(1.1);
        }
        
        .service-content {
            padding: 30px;
        }
        
        .service-content h3 {
            font-size: 1.5rem;
            margin-bottom: 15px;
            color: var(--secondary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .service-content h3 i {
            color: var(--primary);
        }
        
        .service-content ul {
            list-style: none;
            margin-top: 20px;
        }
        
        .service-content ul li {
            margin-bottom: 12px;
            padding-left: 25px;
            position: relative;
        }
        
        .service-content ul li::before {
            content: '✓';
            position: absolute;
            left: 0;
            color: var(--primary);
            font-weight: bold;
        }
        
        /* Gallery Section */
        .gallery {
            padding: 100px 0;
            background: linear-gradient(to bottom, #43484e, #1a1a1a);
            color: white;
        }
        
        .gallery-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
        }
        
        .gallery-item {
            position: relative;
            overflow: hidden;
            border-radius: 10px;
            height: 300px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s;
        }
        
        .gallery-item:hover img {
            transform: scale(1.1);
        }
        
        .gallery-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
            color: white;
            padding: 25px 20px;
            opacity: 0;
            transition: opacity 0.3s;
            transform: translateY(20px);
        }
        
        .gallery-item:hover .gallery-overlay {
            opacity: 1;
            transform: translateY(0);
        }
        
        .gallery-overlay h3 {
            margin-bottom: 10px;
            font-size: 1.3rem;
        }
        
        /* Process Section */
        .process {
            padding: 100px 0;
            background-color: white;
        }
        
        .process-steps {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 30px;
            margin-top: 50px;
        }
        
        .step {
            flex: 1;
            min-width: 250px;
            max-width: 300px;
            text-align: center;
            padding: 40px 20px;
            border-radius: 10px;
            background-color: var(--light);
            position: relative;
            transition: all 0.3s;
        }
        
        .step:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }
        
        .step-number {
            position: absolute;
            top: -20px;
            left: 50%;
            transform: translateX(-50%);
            width: 50px;
            height: 50px;
            background-color: var(--primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .step h3 {
            margin: 20px 0 15px;
            color: var(--secondary);
            font-size: 1.4rem;
        }
        
        /* Contact Section */
        .contact {
            padding: 100px 0;
            background: linear-gradient(rgba(44, 62, 80, 0.9), rgba(44, 62, 80, 0.9)), url('https://images.unsplash.com/photo-1485291571150-772bcfc10da5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2000&q=80');
            background-size: cover;
            background-position: center;
            color: white;
            text-align: center;
        }
        
        .contact-container {
            max-width: 700px;
            margin: 0 auto;
        }
        
        .contact-form {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-top: 40px;
        }
        
        .contact-form input,
        .contact-form textarea,
        .contact-form select {
            width: 100%;
            padding: 15px;
            border-radius: 8px;
            border: none;
            background-color: rgba(255, 255, 255, 0.9);
            font-size: 1rem;
        }
        
        .contact-form textarea {
            grid-column: span 2;
            height: 150px;
            resize: vertical;
        }
        
        .contact-form .full-width {
            grid-column: span 2;
        }
        
        /* Footer */
        footer {
            background-color: var(--dark);
            color: #b4abab;
            padding: 60px 0 30px;
        }
        
        .footer-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
            margin-bottom: 40px;
        }
        
        .footer-column h3 {
            font-size: 1.4rem;
            margin-bottom: 25px;
            color: var(--primary);
            position: relative;
            padding-bottom: 10px;
        }
        
        .footer-column h3::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 50px;
            height: 3px;
            background-color: var(--primary);
        }
        
        .footer-column ul {
            list-style: none;
        }
        
        .footer-column ul li {
            margin-bottom: 15px;
        }
        
        .footer-column ul li a {
            color: #ccc;
            text-decoration: none;
            transition: color 0.3s;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .footer-column ul li a:hover {
            color: var(--primary);
        }
        
        .social-icons {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }
        
        .social-icons a {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            background-color: #333;
            color: white;
            border-radius: 50%;
            transition: all 0.3s;
        }
        
        .social-icons a:hover {
            background-color: var(--primary);
            transform: translateY(-5px);
        }
        
        .copyright {
            text-align: center;
            padding-top: 30px;
            border-top: 1px solid #444;
            font-size: 0.9rem;
        }
        
        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        /* Responsive */
        @media (max-width: 992px) {
            .hero h1 {
                font-size: 2.8rem;
            }
            
            .hero p {
                font-size: 1.2rem;
            }
            
            nav ul {
                gap: 20px;
            }
        }
        
        @media (max-width: 768px) {
            .mobile-menu {
                display: block;
            }
            
            nav ul {
                position: fixed;
                top: 70px;
                left: -100%;
                flex-direction: column;
                background-color: var(--secondary);
                width: 100%;
                text-align: center;
                padding: 20px 0;
                gap: 15px;
                transition: 0.3s;
            }
            
            nav ul.active {
                left: 0;
            }
            
            .hero h1 {
                font-size: 2.3rem;
            }
            
            .hero p {
                font-size: 1.1rem;
            }
            
            .contact-form {
                grid-template-columns: 1fr;
            }
            
            .contact-form textarea,
            .contact-form .full-width {
                grid-column: span 1;
            }
        }
        
        @media (max-width: 480px) {
            .logo h1 {
                font-size: 1.5rem;
            }
            
            .hero h1 {
                font-size: 2rem;
            }
            
            .btn {
                padding: 12px 30px;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container header-container">
            <div class="logo">
                <i class="fas fa-car"></i>
                <h1>TDD<span>VEICULOS</span></h1>
            </div>
            <div class="mobile-menu">
                <i class="fas fa-bars"></i>
            </div>
            <nav>
                <ul>
                    <li><a href="#home">Início</a></li>
                    <li><a href="#services">Serviços</a></li>
                    <li><a href="#gallery">Galeria</a></li>
                    <li><a href="#process">Processo</a></li>
                    <li><a href="#contact">Orçamento</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero" id="home">
        <div class="container">
            <div class="hero-content">
                <h1>Transforme seu veículo em uma obra de arte</h1>
                <p>Personalização premium para quem busca exclusividade e alto desempenho</p>
                <a href="#contact" class="btn">Solicite seu Orçamento</a>
            </div>
        </div>
    </section>

    <!-- Services Section -->
    <section class="services" id="services">
        <div class="container">
            <div class="section-title">
                <h2>Nossos Serviços</h2>
                <p>Oferecemos personalizações completas que transformam seu veículo em uma máquina única</p>
            </div>
            
            <div class="services-grid">
                <!-- Service 1 -->
                <div class="service-card">
                    <div class="service-img">
                        <img src="https://images.unsplash.com/photo-1583121274602-3e2820c69888?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Personalização Externa">
                    </div>
                    <div class="service-content">
                        <h3><i class="fas fa-spray-can"></i> Personalização Externa</h3>
                        <p>Transforme a aparência externa do seu veículo com nossos serviços premium:</p>
                        <ul>
                            <li>Pintura especial (perolizada, cromada, fosca)</li>
                            <li>Adesivagem e vinilização completa</li>
                            <li>Rodas esportivas personalizadas</li>
                            <li>Kits aerodinâmicos exclusivos</li>
                            <li>Iluminação LED personalizada</li>
                        </ul>
                    </div>
                </div>
                
                <!-- Service 2 -->
                <div class="service-card">
                    <div class="service-img">
                        <img src="https://images.unsplash.com/photo-1552519507-da3b142c6e3d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Personalização Interna">
                    </div>
                    <div class="service-content">
                        <h3><i class="fas fa-couch"></i> Personalização Interna</h3>
                        <p>Conforto e luxo no interior do seu veículo:</p>
                        <ul>
                            <li>Bancos em couro premium personalizados</li>
                            <li>Painéis em fibra de carbono ou madeira nobre</li>
                            <li>Iluminação ambiente personalizável</li>
                            <li>Sistemas de som de alta performance</li>
                            <li>Volantes e pedais esportivos</li>
                        </ul>
                    </div>
                </div>
                
                <!-- Service 3 -->
                <div class="service-card">
                    <div class="service-img">
                        <img src="https://images.unsplash.com/photo-1514867644123-6385d58d3cd4?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1074&q=80" alt="Performance">
                    </div>
                    <div class="service-content">
                        <h3><i class="fas fa-tachometer-alt"></i> Performance</h3>
                        <p>Potencialize seu veículo para alto desempenho:</p>
                        <ul>
                            <li>Chip tuning e reprogramação eletrônica</li>
                            <li>Preparação de motores</li>
                            <li>Suspensão esportiva e a ar</li>
                            <li>Sistemas de escape esportivo</li>
                            <li>Freios de alto desempenho</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Gallery Section -->
    <section class="gallery" id="gallery">
        <div class="container">
            <div class="section-title">
                <h2>Nossos Trabalhos</h2>
                <p>Veja alguns dos projetos exclusivos que transformamos para nossos clientes</p>
            </div>
            
            <div class="gallery-container">
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1617814076367-b759c7d7e738?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Projeto 1">
                    <div class="gallery-overlay">
                        <h3>Mustang GT Premium</h3>
                        <p>Pintura perolizada + Rodas 20"</p>
                    </div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1618843479313-40f8afb4b4d8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Projeto 2">
                    <div class="gallery-overlay">
                        <h3>BMW M4 Competition</h3>
                        <p>Kit aerodinâmico + Escape esportivo</p>
                    </div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1617531653332-0e0f03334a98?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Projeto 3">
                    <div class="gallery-overlay">
                        <h3>Porsche 911 Turbo S</h3>
                        <p>Interior em couro premium + Fibra de carbono</p>
                    </div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1580273916550-e323be2ae537?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Projeto 4">
                    <div class="gallery-overlay">
                        <h3>Land Rover Defender</h3>
                        <p>Personalização off-road completa</p>
                    </div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1617814076367-b759c7d7e738?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Projeto 5">
                    <div class="gallery-overlay">
                        <h3>Audi R8 V10</h3>
                        <p>Vinilização completa + Suspensão a ar</p>
                    </div>
                </div>
                
                <div class="gallery-item">
                    <img src="https://images.unsplash.com/photo-1580273916550-e323be2ae537?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80" alt="Projeto 6">
                    <div class="gallery-overlay">
                        <h3>Mercedes AMG GT</h3>
                        <p>Preparação de motor + Freios esportivos</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Process Section -->
    <section class="process" id="process">
        <div class="container">
            <div class="section-title">
                <h2>Como Funciona</h2>
                <p>Nosso processo de personalização passo a passo</p>
            </div>
            
            <div class="process-steps">
                <div class="step">
                    <div class="step-number">1</div>
                    <i class="fas fa-comments fa-3x" style="color: #746d68;"></i>
                    <h3>Consulta</h3>
                    <p>Discutimos suas ideias e necessidades para entender sua visão do projeto</p>
                </div>
                
                <div class="step">
                    <div class="step-number">2</div>
                    <i class="fas fa-drafting-compass fa-3x" style="color: #8a8785;"></i>
                    <h3>Projeto 3D</h3>
                    <p>Criamos uma simulação 3D do resultado final para sua aprovação</p>
                </div>
                
                <div class="step">
                    <div class="step-number">3</div>
                    <i class="fas fa-check-circle fa-3x" style="color: #7a7877;"></i>
                    <h3>Aprovação</h3>
                    <p>Você analisa e aprova o projeto, ou solicita ajustes</p>
                </div>
                
                <div class="step">
                    <div class="step-number">4</div>
                    <i class="fas fa-tools fa-3x" style="color: #474646;"></i>
                    <h3>Execução</h3>
                    <p>Nossos especialistas transformam seu veículo com materiais premium</p>
                </div>
                
                <div class="step">
                    <div class="step-number">5</div>
                    <i class="fas fa-car fa-3x" style="color: #494949;"></i>
                    <h3>Entrega</h3>
                    <p>Você recebe seu veículo exclusivo com garantia e suporte</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section class="contact" id="contact">
        <div class="container">
            <div class="contact-container">
                <div class="section-title">
                    <h2>Solicite seu Orçamento</h2>
                    <p>Preencha o formulário e transforme seu veículo em uma máquina exclusiva</p>
                </div>
                
                <form class="contact-form">
                    <input type="text" placeholder="Nome Completo" required>
                    <input type="email" placeholder="E-mail" required>
                    <input type="tel" placeholder="Telefone" required>
                    <input type="text" placeholder="Modelo do Veículo" required>
                    
                    <select required>
                        <option value="" disabled selected>Tipo de Personalização</option>
                        <option value="external">Personalização Externa</option>
                        <option value="internal">Personalização Interna</option>
                        <option value="performance">Performance</option>
                        <option value="complete">Personalização Completa</option>
                    </select>
                    
                    <select required>
                        <option value="" disabled selected>Orçamento Aproximado</option>
                        <option value="5-10">R$5.000 - R$10.000</option>
                        <option value="10-20">R$10.000 - R$20.000</option>
                        <option value="20-50">R$20.000 - R$50.000</option>
                        <option value="50+">Acima de R$50.000</option>
                    </select>
                    
                    <textarea placeholder="Descreva sua ideia de personalização..." required></textarea>
                    
                    <div class="full-width">
                        <button type="submit" class="btn">Solicitar Orçamento</button>
                    </div>
                </form>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-container">
                <div class="footer-column">
                    <h3>AutoElite</h3>
                    <p>Transformando veículos comuns em máquinas exclusivas desde 2010. Qualidade, inovação e exclusividade em cada projeto.</p>
                    <div class="social-icons">
                        <a href="#"><i class="fab fa-facebook-f"></i></a>
                        <a href="#"><i class="fab fa-instagram"></i></a>
                        <a href="#"><i class="fab fa-youtube"></i></a>
                        <a href="#"><i class="fab fa-whatsapp"></i></a>
                    </div>
                </div>
                
                <div class="footer-column">
                    <h3>Links Rápidos</h3>
                    <ul>
                        <li><a href="#home"><i class="fas fa-chevron-right"></i> Início</a></li>
                        <li><a href="#services"><i class="fas fa-chevron-right"></i> Serviços</a></li>
                        <li><a href="#gallery"><i class="fas fa-chevron-right"></i> Galeria</a></li>
                        <li><a href="#process"><i class="fas fa-chevron-right"></i> Processo</a></li>
                        <li><a href="#contact"><i class="fas fa-chevron-right"></i> Orçamento</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h3>Serviços</h3>
                    <ul>
                        <li><a href="#"><i class="fas fa-chevron-right"></i> Personalização Externa</a></li>
                        <li><a href="#"><i class="fas fa-chevron-right"></i> Personalização Interna</a></li>
                        <li><a href="#"><i class="fas fa-chevron-right"></i> Performance</a></li>
                        <li><a href="#"><i class="fas fa-chevron-right"></i> Manutenção Premium</a></li>
                        <li><a href="#"><i class="fas fa-chevron-right"></i> Consultoria Especializada</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h3>Contato</h3>
                    <ul>
                        <li><a href="#"><i class="fas fa-map-marker-alt"></i> Av. Automotiva, 1234 - São Paulo, SP</a></li>
                        <li><a href="tel:+5511999999999"><i class="fas fa-phone"></i> (11) 99999-9999</a></li>
                        <li><a href="mailto:contato@autoelite.com.br"><i class="fas fa-envelope"></i> contato@autoelite.com.br</a></li>
                        <li><a href="#"><i class="fas fa-clock"></i> Seg-Sex: 9h às 18h | Sáb: 9h às 13h</a></li>
                    </ul>
                </div>
            </div>
            
            <div class="copyright">
                <p>&copy; 2023 AutoElite - Concessionária de Veículos Personalizados. Todos os direitos reservados.</p>
            </div>
        </div>
    </footer>

    <script>
        // Mobile Menu Toggle
        const mobileMenu = document.querySelector('.mobile-menu');
        const navMenu = document.querySelector('nav ul');
        
        mobileMenu.addEventListener('click', () => {
            navMenu.classList.toggle('active');
        });
        
        // Smooth Scrolling
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                
                navMenu.classList.remove('active');
                
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });
        
        // Animation on Scroll
        const observerOptions = {
            root: null,
            rootMargin: '0px',
            threshold: 0.1
        };
        
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('animated');
                }
            });
        }, observerOptions);
        
        document.querySelectorAll('.service-card, .step, .gallery-item').forEach(el => {
            observer.observe(el);
        });
    </script>
</body>
</html>
