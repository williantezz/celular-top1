# celular-top1<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menu de Celulares</title>
    <style>
        /* Estilos Gerais */
        body {
            font-family: 'Inter', sans-serif; /* Fonte premium */
            margin: 0;
            padding: 20px;
            background-color: #1a1a2e; /* Fundo escuro premium */
            color: #e0e0e0; /* Cor do texto claro para contraste */
            line-height: 1.6;
            display: flex; /* Usar flexbox para centralizar o conteúdo principal */
            flex-direction: column;
            align-items: center; /* Centraliza horizontalmente */
            min-height: 100vh; /* Garante que o body ocupe a altura total da viewport */
        }

        /* Container principal para limitar a largura da página */
        .main-container {
            width: 100%;
            max-width: 1200px; /* Largura máxima para a página web */
            padding: 0 20px; /* Padding nas laterais para telas maiores */
            box-sizing: border-box; /* Inclui padding na largura total */
        }

        h1, h2, h3 {
            color: #e0e0e0; /* Títulos claros */
            text-align: center; /* Centraliza títulos */
        }

        /* Estilos do Menu */
        .menu-section {
            margin-bottom: 40px;
            padding: 20px;
            background-color: #21213e; /* Fundo mais claro para seções */
            border-radius: 12px; /* Cantos mais arredondados */
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3); /* Sombra mais pronunciada */
            width: 100%; /* Garante que a seção ocupe a largura total do main-container */
            box-sizing: border-box;
        }
        .menu-section h2 {
            color: #8be9fd; /* Cor de destaque para os títulos das seções */
            border-bottom: 2px solid #8be9fd;
            padding-bottom: 10px;
            margin-bottom: 25px;
            font-size: 1.8em;
        }
        .phone-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); /* Ajuste para cards um pouco maiores */
            gap: 25px; /* Espaçamento maior entre os cards */
        }
        .phone-card {
            background-color: #282a4a; /* Fundo dos cards */
            border: 1px solid #3a3f67; /* Borda sutil */
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.3s ease;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            display: flex; /* Para centralizar conteúdo verticalmente */
            flex-direction: column;
            justify-content: space-between; /* Espaço entre título, imagem e preço */
        }
        .phone-card:hover {
            transform: translateY(-8px); /* Efeito de elevação mais pronunciado */
            box-shadow: 0 12px 24px rgba(0,0,0,0.4); /* Sombra maior no hover */
            background-color: #31345c; /* Fundo do card mais claro no hover */
        }
        .phone-card img {
            max-width: 100%;
            height: 180px; /* Altura fixa para imagens */
            object-fit: contain; /* Garante que a imagem se ajuste sem cortar */
            border-radius: 8px;
            margin-bottom: 15px;
            background-color: #fff; /* Fundo branco para imagens */
            padding: 5px; /* Pequeno padding para as imagens */
        }
        .phone-card h3 {
            font-size: 1.2em;
            margin-bottom: 10px;
            color: #e0e0e0;
        }
        .phone-card p {
            font-size: 1em;
            color: #bbbbbb; /* Cor mais clara para o preço */
            font-weight: bold;
        }

        /* Pop-up base styles */
        .popup-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8); /* Fundo mais escuro para o overlay */
            justify-content: center;
            align-items: center;
            z-index: 1000;
            backdrop-filter: blur(5px); /* Efeito de desfoque */
        }
        .popup-content {
            background: #21213e; /* Fundo do pop-up */
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.4);
            max-width: 700px; /* Largura maior para o pop-up */
            width: 90%;
            text-align: left;
            position: relative;
            color: #e0e0e0;
            max-height: 90vh; /* Limita a altura do popup */
            overflow-y: auto; /* Adiciona scroll se o conteúdo for muito grande */
        }
        .popup-content h3 {
            margin-top: 0;
            color: #8be9fd;
            border-bottom: 1px solid #3a3f67;
            padding-bottom: 10px;
            margin-bottom: 20px;
            font-size: 1.6em;
        }
        .popup-content p {
            margin-bottom: 10px;
            line-height: 1.6;
            color: #bbbbbb;
        }
        .popup-buttons {
            margin-top: 30px;
            display: flex;
            justify-content: space-around;
            gap: 20px;
        }
        .popup-buttons button {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.1em;
            flex: 1;
            font-weight: bold;
            transition: background-color 0.3s ease, transform 0.2s ease;
        }
        .popup-buttons .back-button {
            background-color: #6c757d;
            color: white;
        }
        .popup-buttons .back-button:hover {
            background-color: #5a6268;
            transform: translateY(-2px);
        }
        .popup-buttons .buy-button {
            background-color: #007bff;
            color: white;
        }
        .popup-buttons .buy-button:hover {
            background-color: #0056b3;
            transform: translateY(-2px);
        }

        /* Payment selection popup */
        .payment-popup-content {
            text-align: center;
        }
        .payment-popup-content button {
            padding: 18px 40px;
            margin: 15px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.3em;
            background-color: #28a745;
            color: white;
            transition: background-color 0.3s ease, transform 0.2s ease;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        .payment-popup-content button:hover {
            background-color: #218838;
            transform: translateY(-2px);
        }

        /* Registration form popup */
        .registration-form-content {
            text-align: left;
        }
        .registration-form-content label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #e0e0e0;
        }
        .registration-form-content input[type="text"],
        .registration-form-content input[type="file"],
        .registration-form-content input[type="email"] {
            width: calc(100% - 24px); /* Ajuste para padding */
            padding: 12px;
            margin-bottom: 20px;
            border: 1px solid #3a3f67;
            border-radius: 6px;
            background-color: #282a4a; /* Fundo dos inputs */
            color: #e0e0e0; /* Cor do texto nos inputs */
        }
        .registration-form-content input[type="file"] {
            padding: 10px; /* Ajuste para inputs de arquivo */
        }
        .registration-form-content .file-upload-section {
            margin-top: 25px;
            border-top: 1px solid #3a3f67;
            padding-top: 25px;
        }
        .registration-form-content .form-buttons {
            display: flex;
            justify-content: space-between;
            gap: 10px;
            margin-top: 30px;
        }
        .registration-form-content .form-buttons button {
            padding: 18px;
            border: none;
            border-radius: 8px;
            font-size: 1.3em;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.3s ease, transform 0.2s ease;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            flex: 1; /* Para os botões ocuparem espaço igual */
        }
        .registration-form-content .form-buttons .submit-button {
            background-color: #007bff;
            color: white;
        }
        .registration-form-content .form-buttons .submit-button:hover {
            background-color: #0056b3;
            transform: translateY(-2px);
        }
        .registration-form-content .form-buttons .close-button {
            background-color: #dc3545; /* Cor vermelha para fechar */
            color: white;
        }
        .registration-form-content .form-buttons .close-button:hover {
            background-color: #c82333;
            transform: translateY(-2px);
        }

        /* Media Queries para Responsividade */

        /* Para telas menores que 768px (tablets e celulares) */
        @media (max-width: 768px) {
            body {
                padding: 10px; /* Reduz o padding geral em telas menores */
            }

            .main-container {
                padding: 0 10px; /* Reduz o padding do container principal */
            }

            .menu-section {
                padding: 15px; /* Reduz o padding das seções */
            }

            .menu-section h2 {
                font-size: 1.5em; /* Ajusta o tamanho da fonte dos títulos das seções */
                margin-bottom: 20px;
            }

            .phone-grid {
                grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); /* 2 colunas em telas menores */
                gap: 15px; /* Reduz o espaçamento entre os cards */
            }

            .phone-card {
                padding: 15px; /* Reduz o padding dos cards */
            }

            .phone-card img {
                height: 150px; /* Ajusta a altura da imagem para telas menores */
            }

            .phone-card h3 {
                font-size: 1.1em; /* Ajusta o tamanho da fonte do título do card */
            }

            .phone-card p {
                font-size: 0.9em; /* Ajusta o tamanho da fonte do preço */
            }

            .popup-content {
                padding: 20px; /* Reduz o padding do pop-up */
                width: 95%; /* Ocupa mais largura em telas menores */
                max-height: 85vh; /* Ajusta a altura máxima do pop-up */
            }

            .popup-content h3 {
                font-size: 1.4em; /* Ajusta o tamanho da fonte do título do pop-up */
            }

            .popup-buttons button,
            .payment-popup-content button,
            .registration-form-content .form-buttons button {
                padding: 12px 20px; /* Reduz o padding dos botões */
                font-size: 1em; /* Ajusta o tamanho da fonte dos botões */
            }

            .registration-form-content input[type="text"],
            .registration-form-content input[type="file"],
            .registration-form-content input[type="email"] {
                padding: 10px; /* Reduz o padding dos inputs */
                margin-bottom: 15px;
            }

            .registration-form-content .form-buttons {
                flex-direction: column; /* Botões em coluna no mobile */
                gap: 10px;
            }
        }

        /* Para telas muito pequenas (celulares em modo retrato) */
        @media (max-width: 480px) {
            .phone-grid {
                grid-template-columns: 1fr; /* Uma única coluna em telas muito pequenas */
            }

            .phone-card img {
                height: 200px; /* Pode aumentar a altura da imagem para preencher melhor */
            }
        }
    </style>
</head>
<body>

    <div class="main-container">
        <h1>Menu de Celulares</h1>

        <div class="menu-section">
            <h2>🔥 Top de Linha – Alto Desempenho</h2>
            <div class="phone-grid">
                <div class="phone-card" data-model="Redmi Note 13 Pro">
                    <img src="note 13 Pro 4g.jpeg" alt="Redmi Note 13 Pro">
                    <h3>Redmi Note 13 Pro – 512GB + 12GB RAM</h3>
                    <p>Valor: R$400 de entrada + 7x de R$300 (semanal)</p>
                </div>
                <div class="phone-card" data-model="Realme 12 5G">
                    <img src="Realme 12 5G RMX3999 512GB 8GB RAM.webp" alt="Realme 12 5G">
                    <h3>Realme 12 5G – 512GB + 16GB RAM</h3>
                    <p>Valor: R$400 de entrada + 7x de R$300 (semanal)</p>
                </div>
                <div class="phone-card" data-model="Poco X7 5G">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Poco+X7+5G" alt="Poco X7 5G">
                    <h3>Poco X7 5G – 256GB + 8GB RAM</h3>
                    <p>Valor: R$400 de entrada + 7x de R$300 (semanal)</p>
                </div>
            </div>
        </div>

        <div class="menu-section">
            <h2>🔥 256GB + 8GB RAM</h2>
            <div class="phone-grid">
                <div class="phone-card" data-model="Realme C61 256GB">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Realme+C61" alt="Realme C61">
                    <h3>Realme C61 – 256GB + 8GB RAM</h3>
                    <p>Valor: 6x de R$300 (semanal) ou 30x de R$60 (diária)</p>
                </div>
                <div class="phone-card" data-model="Redmi Note 13 5G">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+Note+13+5G" alt="Redmi Note 13 5G">
                    <h3>Redmi Note 13 5G – 256GB + 8GB RAM</h3>
                    <p>Valor: 6x de R$300 (semanal) ou 30x de R$60 (diária)</p>
                </div>
                <div class="phone-card" data-model="Poco C75 256GB">
                    <img src="poco c75 256g 8 ram.webp" alt="Poco C75">
                    <h3>Poco C75 – 256GB + 8GB RAM</h3>
                    <p>Valor: 6x de R$400 (semanal) ou 30x de R$90 (diária)</p>
                </div>
                <div class="phone-card" data-model="Redmi 14C 256GB">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+14C" alt="Redmi 14C">
                    <h3>Redmi 14C – 256GB + 8GB RAM</h3>
                    <p>Valor: 7x de R$300 (semanal) ou 30x de R$70 (diária)</p>
                </div>
                <div class="phone-card" data-model="Redmi 13">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+13" alt="Redmi 13">
                    <h3>Redmi 13 – 256GB + 8GB RAM</h3>
                    <p>Valor: 6x de R$330 (semanal) ou 30x de R$65 (diária)</p>
                </div>
                <div class="phone-card" data-model="Realme C67">
                    <img src="Realme C67 Dual SIM 256 GB.webp" alt="Realme C67">
                    <h3>Realme C67 – 256GB + 8GB RAM</h3>
                    <p>Valor: 7x de R$300 (semanal) ou 30x de R$70 (diária)</p>
                </div>
                <div class="phone-card" data-model="Realme C63">
                    <img src="Realme C63 NFC 256GB + 12GB RAM.webp" alt="Realme C63">
                    <h3>Realme C63 – 256GB + 8GB RAM</h3>
                    <p>Valor: 7x de R$300 (semanal) ou 30x de R$70 (diária)</p>
                </div>
                <div class="phone-card" data-model="Redmi Note 14">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+Note+14" alt="Redmi Note 14">
                    <h3>Redmi Note 14 – 256GB + 8GB RAM</h3>
                    <p>Valor: 7x de R$310 (semanal) ou 30x de R$72 (diária)</p>
                </div>
                <div class="phone-card" data-model="Infinix Hot 50 Pro">
                    <img src="Infinix Hot 50 Pro 4G 256GB  8GB RAM.webp" alt="Infinix Hot 50 Pro">
                    <h3>Infinix Hot 50 Pro – 256GB + 8GB RAM</h3>
                    <p>Valor: 7x de R$300 (semanal) ou 30x de R$70 (diária)</p>
                </div>
            </div>
        </div>

        <div class="menu-section">
            <h2>� 128GB (4GB ou 6GB RAM)</h2>
            <div class="phone-grid">
                <div class="phone-card" data-model="Realme C61 128GB">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Realme+C61+128GB" alt="Realme C61 128GB">
                    <h3>Realme C61 – 128GB + 4GB RAM</h3>
                    <p>Valor: 6x de R$250 (semanal) ou 30x de R$50 (diária)</p>
                </div>
                <div class="phone-card" data-model="Realme Note 60">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Realme+Note+60" alt="Realme Note 60">
                    <h3>Realme Note 60 – 128GB + 4GB RAM</h3>
                    <p>Valor: 6x de R$220 (semanal) ou 30x de R$45 (diária)</p>
                </div>
                <div class="phone-card" data-model="Redmi 14C 128GB 4GB RAM">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+14C+128GB+4GB" alt="Redmi 14C 128GB 4GB RAM">
                    <h3>Redmi 14C – 128GB + 4GB RAM</h3>
                    <p>Valor: 6x de R$220 (semanal) ou 30x de R$45 (diária)</p>
                </div>
                <div class="phone-card" data-model="Redmi 14C 128GB 6GB RAM">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+14C+128GB+6GB" alt="Redmi 14C 128GB 6GB RAM">
                    <h3>Redmi 14C – 128GB + 6GB RAM</h3>
                    <p>Valor: 6x de R$250 (semanal) ou 30x de R$50 (diária)</p>
                </div>
                <div class="phone-card" data-model="Poco C71">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Poco+C71" alt="Poco C71">
                    <h3>Poco C71 – 128GB + 4GB RAM</h3>
                    <p>Valor: 6x de R$200 (semanal) ou 30x de R$40 (diária)</p>
                </div>
                <div class="phone-card" data-model="Redmi A5">
                    <img src="https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+A5" alt="Redmi A5">
                    <h3>Redmi A5 – 128GB + 4GB RAM (+4GB Expansão)</h3>
                    <p>Valor: 6x de R$200 (semanal) ou 30x de R$40 (diária)</p>
                </div>
                <div class="phone-card" data-model="Xiaomi Poco C75 128GB">
                    <img src="poco c75 256g 8 ram.webp" alt="Xiaomi Poco C75">
                    <h3>Xiaomi Poco C75 – 128GB + 6GB RAM</h3>
                    <p>Valor: 6x de R$280 (semanal) ou 30x de R$56 (diária)</p>
                </div>
                <div class="phone-card" data-model="Iteo P55">
                    <img src="itel P55 5G ( 128 GB Storage, 6 GB RAM ).webp" alt="Iteo P55">
                    <h3>Iteo P55 – 128GB + 6GB RAM</h3>
                    <p>Valor: 6x de R$270 (semanal) ou 30x de R$54 (diária)</p>
                </div>
                <div class="phone-card" data-model="Infinix Smart 9">
                    <img src="Infinix Smart 9, Câmera 13MP, 128GB  4GB RAM.webp" alt="Infinix Smart 9">
                    <h3>Infinix Smart 9 – 128GB + 4GB RAM</h3>
                    <p>Valor: 6x de R$200 (semanal) ou 30x de R$40 (diária)</p>
                </div>
                <div class="phone-card" data-model="Cell e Tel A70">
                    <img src="Itel A70 256GB 4GB RAM.webp" alt="Cell e Tel A70">
                    <h3>Cell e Tel A70 – 128GB + 4GB RAM</h3>
                    <p>Valor: 6x de R$220 (semanal) ou 30x de R$45 (diária)</p>
                </div>
            </div>
        </div>
    </div>

    <div id="techSpecPopup" class="popup-overlay">
        <div class="popup-content">
            <h3 id="popupModelName"></h3>
            <div id="techSpecsContent"></div>
            <div class="popup-buttons">
                <button class="back-button" onclick="closePopup('techSpecPopup')">Voltar</button>
                <button class="buy-button" onclick="showPaymentOptions()">Comprar</button>
            </div>
        </div>
    </div>

    <div id="paymentOptionsPopup" class="popup-overlay">
        <div class="popup-content payment-popup-content">
            <h3>Selecione o Modo de Pagamento</h3>
            <button onclick="showRegistrationForm('semanal')">Semanal</button>
            <button onclick="showRegistrationForm('diaria')">Diária</button>
        </div>
    </div>

    <div id="registrationFormPopup" class="popup-overlay">
        <div class="popup-content registration-form-content">
            <h3>Cadastro para Compra</h3>
            <form id="registrationForm">
                <label for="fullName">Nome Completo:</label>
                <input type="text" id="fullName" name="fullName" required>

                <label for="cpf">CPF:</label>
                <input type="text" id="cpf" name="cpf" required>

                <label for="phone">Telefone:</label>
                <input type="text" id="phone" name="phone" required>

                <label for="address">Endereço Completo:</label>
                <input type="text" id="address" name="address" required>

                <label for="cep">CEP:</label>
                <input type="text" id="cep" name="cep" required>

                <label for="socialMedia">@ de Rede Social:</label>
                <input type="text" id="socialMedia" name="socialMedia" required>

                <div class="file-upload-section">
                    <label for="rgCnh">RG ou CNH (upload):</label>
                    <input type="file" id="rgCnh" name="rgCnh" accept=".pdf,.jpg,.jpeg,.png" required>

                    <label for="proofOfResidence">Comprovante de Residência (upload):</label>
                    <input type="file" id="proofOfResidence" name="proofOfResidence" accept=".pdf,.jpg,.jpeg,.png" required>

                    <label for="selfieWithDoc">Selfie com Documento (upload):</label>
                    <input type="file" id="selfieWithDoc" name="selfieWithDoc" accept=".jpg,.jpeg,.png" required>

                    <label for="socialMediaPrint">Print do Perfil de Rede Social (upload):</label>
                    <input type="file" id="socialMediaPrint" name="socialMediaPrint" accept=".jpg,.jpeg,.png" required>
                </div>

                <div class="form-buttons">
                    <button type="submit" class="submit-button">Finalizar e Enviar Cadastro</button>
                    <button type="button" class="close-button" onclick="closePopup('registrationFormPopup')">Fechar</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        const phoneData = {
            "Redmi Note 13 Pro": {
                specs: `
                    ▪️ Tela: AMOLED 6.67” FHD+ 120Hz<br>
                    ▪️ Processador: Snapdragon 7s Gen 2<br>
                    ▪️ Câmera: 200MP + 8MP + 2MP | Frontal 16MP<br>
                    ▪️ Bateria: 5100mAh com carregamento 67W<br>
                    ▪️ Conectividade: 5G<br>
                    ▪️ Extras: Leitor digital na tela, NFC<br>
                    ▪️ Valor: R$400 de entrada + 7x de R$300 (semanal)
                `,
                image: "note 13 Pro 4g.jpeg"
            },
            "Realme 12 5G": {
                specs: `
                    ▪️ Tela: IPS LCD 6.72” FHD+ 120Hz<br>
                    ▪️ Processador: Dimensity 6100+<br>
                    ▪️ Câmera: 108MP + 2MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com carregamento 45W<br>
                    ▪️ Conectividade: 5G<br>
                    ▪️ Extras: Leitor digital lateral, IP54<br>
                    ▪️ Valor: R$400 de entrada + 7x de R$300 (semanal)
                `,
                image: "Realme 12 5G RMX3999 512GB 8GB RAM.webp"
            },
            "Poco X7 5G": {
                specs: `
                    ▪️ Tela: AMOLED 6.67” FHD+ 120Hz<br>
                    ▪️ Processador: Snapdragon 695<br>
                    ▪️ Câmera: 64MP + 2MP | Frontal 16MP<br>
                    ▪️ Bateria: 5000mAh com carregamento 33W<br>
                    ▪️ Conectividade: 5G<br>
                    ▪️ Extras: Leitor lateral, IP53<br>
                    ▪️ Valor: R$400 de entrada + 7x de R$300 (semanal)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Poco+X7+5G" // Placeholder
            },
            "Realme C61 256GB": {
                specs: `
                    ▪️ Tela: IPS LCD 6.78” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T612<br>
                    ▪️ Câmera: 50MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 10W<br>
                    ▪️ Extras: Leitor digital lateral, IP54<br>
                    ▪️ Valor: 6x de R$300 (semanal) ou 30x de R$60 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Realme+C61" // Placeholder
            },
            "Redmi Note 13 5G": {
                specs: `
                    ▪️ Tela: AMOLED 6.6” FHD+ 120Hz<br>
                    ▪️ Processador: Dimensity 6100+<br>
                    ▪️ Câmera: 50MP + 2MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com carregamento 33W<br>
                    ▪️ Conectividade: 5G<br>
                    ▪️ Extras: Leitor lateral, IP54<br>
                    ▪️ Valor: 6x de R$300 (semanal) ou 30x de R$60 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+Note+13+5G" // Placeholder
            },
            "Poco C75 256GB": {
                specs: `
                    ▪️ Tela: IPS LCD 6.74” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T606<br>
                    ▪️ Câmera: 50MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 18W<br>
                    ▪️ Extras: Leitor digital lateral<br>
                    ▪️ Valor: 6x de R$400 (semanal) ou 30x de R$90 (diária)
                `,
                image: "poco c75 256g 8 ram.webp"
            },
            "Redmi 14C 256GB": {
                specs: `
                    ▪️ Tela: IPS LCD 6.74” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T612<br>
                    ▪️ Câmera: 50MP + 0.08MP | Frontal 5MP<br>
                    ▪️ Bateria: 5000mAh com 18W<br>
                    ▪️ Extras: Leitor digital lateral<br>
                    ▪️ Valor: 7x de R$300 (semanal) ou 30x de R$70 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+14C" // Placeholder
            },
            "Redmi 13": {
                specs: `
                    ▪️ Tela: IPS LCD 6.79” FHD+ 90Hz<br>
                    ▪️ Processador: MediaTek Helio G88<br>
                    ▪️ Câmera: 108MP + 2MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 33W<br>
                    ▪️ Extras: Leitor lateral, IP53<br>
                    ▪️ Valor: 6x de R$330 (semanal) ou 30x de R$65 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+13" // Placeholder
            },
            "Realme C67": {
                specs: `
                    ▪️ Tela: IPS LCD 6.72” FHD+ 120Hz<br>
                    ▪️ Processador: Snapdragon 685<br>
                    ▪️ Câmera: 108MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 33W<br>
                    ▪️ Extras: Leitor digital lateral, IP54<br>
                    ▪️ Valor: 7x de R$300 (semanal) ou 30x de R$70 (diária)
                `,
                image: "Realme C67 Dual SIM 256 GB.webp"
            },
            "Realme C63": {
                specs: `
                    ▪️ Tela: IPS LCD 6.74” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T612<br>
                    ▪️ Câmera: 50MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 45W<br>
                    ▪️ Extras: Leitor lateral, IP54<br>
                    ▪️ Valor: 7x de R$300 (semanal) ou 30x de R$70 (diária)
                `,
                image: "Realme C63 NFC 256GB + 12GB RAM.webp"
            },
            "Redmi Note 14": {
                specs: `
                    ▪️ Tela: AMOLED 6.67” FHD+ 120Hz<br>
                    ▪️ Processador: Snapdragon 685<br>
                    ▪️ Câmera: 108MP + 2MP | Frontal 16MP<br>
                    ▪️ Bateria: 5000mAh com 33W<br>
                    ▪️ Extras: Leitor digital na tela, IP54<br>
                    ▪️ Valor: 7x de R$310 (semanal) ou 30x de R$72 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+Note+14" // Placeholder
            },
            "Infinix Hot 50 Pro": {
                specs: `
                    ▪️ Tela: IPS LCD 6.78” FHD+ 120Hz<br>
                    ▪️ Processador: Helio G88<br>
                    ▪️ Câmera: 108MP + AI | Frontal 32MP<br>
                    ▪️ Bateria: 5000mAh com 33W<br>
                    ▪️ Extras: Leitor digital lateral<br>
                    ▪️ Valor: 7x de R$300 (semanal) ou 30x de R$70 (diária)
                `,
                image: "Infinix Hot 50 Pro 4G 256GB  8GB RAM.webp"
            },
            "Realme C61 128GB": {
                specs: `
                    ▪️ Tela: IPS LCD 6.78” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T612<br>
                    ▪️ Câmera: 50MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 10W<br>
                    ▪️ Extras: Leitor digital lateral, IP54<br>
                    ▪️ Valor: 6x de R$250 (semanal) ou 30x de R$50 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Realme+C61+128GB" // Placeholder
            },
            "Realme Note 60": {
                specs: `
                    ▪️ Tela: IPS LCD 6.74” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T612<br>
                    ▪️ Câmera: 50MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 45W<br>
                    ▪️ Extras: Leitor lateral<br>
                    ▪️ Valor: 6x de R$220 (semanal) ou 30x de R$45 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Realme+Note+60" // Placeholder
            },
            "Redmi 14C 128GB 4GB RAM": {
                specs: `
                    ▪️ Tela: IPS LCD 6.74” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T612<br>
                    ▪️ Câmera: 50MP + 0.08MP | Frontal 5MP<br>
                    ▪️ Bateria: 5000mAh com 18W<br>
                    ▪️ Extras: Leitor lateral<br>
                    ▪️ Valor: 6x de R$220 (semanal) ou 30x de R$45 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+14C+128GB+4GB" // Placeholder
            },
            "Redmi 14C 128GB 6GB RAM": {
                specs: `
                    ▪️ Tela: IPS LCD 6.74” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T612<br>
                    ▪️ Câmera: 50MP + 0.08MP | Frontal 5MP<br>
                    ▪️ Bateria: 5000mAh com 18W<br>
                    ▪️ Extras: Leitor lateral<br>
                    ▪️ Valor: 6x de R$250 (semanal) ou 30x de R$50 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+14C+128GB+6GB" // Placeholder
            },
            "Poco C71": {
                specs: `
                    ▪️ Tela: IPS LCD 6.71” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T606<br>
                    ▪️ Câmera: 50MP | Frontal 5MP<br>
                    ▪️ Bateria: 5000mAh com 10W<br>
                    ▪️ Extras: Leitor lateral<br>
                    ▪️ Valor: 6x de R$200 (semanal) ou 30x de R$40 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Poco+C71" // Placeholder
            },
            "Redmi A5": {
                specs: `
                    ▪️ Tela: IPS LCD 6.71” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T603<br>
                    ▪️ Câmera: 8MP | Frontal 5MP<br>
                    ▪️ Bateria: 5000mAh com 10W<br>
                    ▪️ Extras: Leitor lateral<br>
                    ▪️ Valor: 6x de R$200 (semanal) ou 30x de R$40 (diária)
                `,
                image: "https://placehold.co/200x180/282a4a/e0e0e0?text=Redmi+A5" // Placeholder
            },
            "Xiaomi Poco C75 128GB": {
                specs: `
                    ▪️ Tela: IPS LCD 6.74” HD+ 90Hz<br>
                    ▪️ Processador: Unisoc T606<br>
                    ▪️ Câmera: 50MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 18W<br>
                    ▪️ Extras: Leitor lateral<br>
                    ▪️ Valor: 6x de R$280 (semanal) ou 30x de R$56 (diária)
                `,
                image: "poco c75 256g 8 ram.webp"
            },
            "Iteo P55": {
                specs: `
                    ▪️ Tela: IPS LCD 6.5” HD+<br>
                    ▪️ Processador: Unisoc SC9863A<br>
                    ▪️ Câmera: 20MP + 2MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh<br>
                    ▪️ Extras: Leitor digital lateral<br>
                    ▪️ Valor: 6x de R$270 (semanal) ou 30x de R$54 (diária)
                `,
                image: "itel P55 5G ( 128 GB Storage, 6 GB RAM ).webp"
            },
            "Infinix Smart 9": {
                specs: `
                    ▪️ Tela: IPS LCD 6.6” HD+ 90Hz<br>
                    ▪️ Processador: Helio G36<br>
                    ▪️ Câmera: 13MP + AI | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh com 10W<br>
                    ▪️ Extras: Leitor lateral<br>
                    ▪️ Valor: 6x de R$200 (semanal) ou 30x de R$40 (diária)
                `,
                image: "Infinix Smart 9, Câmera 13MP, 128GB  4GB RAM.webp"
            },
            "Cell e Tel A70": {
                specs: `
                    ▪️ Tela: IPS LCD 6.5” HD+<br>
                    ▪️ Processador: Unisoc SC9863A<br>
                    ▪️ Câmera: 20MP + 2MP | Frontal 8MP<br>
                    ▪️ Bateria: 5000mAh<br>
                    ▪️ Extras: Leitor digital lateral<br>
                    ▪️ Valor: 6x de R$220 (semanal) ou 30x de R$45 (diária)
                `,
                image: "Itel A70 256GB 4GB RAM.webp"
            }
        };

        let selectedModel = '';
        let selectedPaymentMode = '';

        document.querySelectorAll('.phone-card').forEach(card => {
            card.addEventListener('click', function() {
                selectedModel = this.dataset.model;
                const modelInfo = phoneData[selectedModel];
                if (modelInfo) {
                    document.getElementById('popupModelName').innerText = selectedModel;
                    document.getElementById('techSpecsContent').innerHTML = modelInfo.specs;
                    document.getElementById('techSpecPopup').style.display = 'flex';
                }
            });
        });

        function closePopup(popupId) {
            document.getElementById(popupId).style.display = 'none';
        }

        function showPaymentOptions() {
            closePopup('techSpecPopup');
            document.getElementById('paymentOptionsPopup').style.display = 'flex';
        }

        function showRegistrationForm(paymentMode) {
            selectedPaymentMode = paymentMode;
            closePopup('paymentOptionsPopup');
            document.getElementById('registrationFormPopup').style.display = 'flex';
        }

        document.getElementById('registrationForm').addEventListener('submit', function(event) {
            event.preventDefault(); // Impede o envio padrão do formulário

            const formData = {
                model: selectedModel,
                paymentMode: selectedPaymentMode,
                fullName: document.getElementById('fullName').value,
                cpf: document.getElementById('cpf').value,
                phone: document.getElementById('phone').value,
                address: document.getElementById('address').value,
                cep: document.getElementById('cep').value,
                socialMedia: document.getElementById('socialMedia').value,
                rgCnh: document.getElementById('rgCnh').files[0] ? document.getElementById('rgCnh').files[0].name : 'Nenhum arquivo',
                proofOfResidence: document.getElementById('proofOfResidence').files[0] ? document.getElementById('proofOfResidence').files[0].name : 'Nenhum arquivo',
                selfieWithDoc: document.getElementById('selfieWithDoc').files[0] ? document.getElementById('selfieWithDoc').files[0].name : 'Nenhum arquivo',
                socialMediaPrint: document.getElementById('socialMediaPrint').files[0] ? document.getElementById('socialMediaPrint').files[0].name : 'Nenhum arquivo'
            };

            console.log("Dados do Cadastro:", formData);

            // Construir a mensagem para o WhatsApp
            let whatsappMessage = `*Novo Cadastro de Celular*\n\n`;
            whatsappMessage += `*Modelo Escolhido:* ${formData.model}\n`;
            whatsappMessage += `*Modo de Pagamento:* ${formData.paymentMode}\n\n`;
            whatsappMessage += `*Dados Pessoais:*\n`;
            whatsappMessage += `Nome Completo: ${formData.fullName}\n`;
            whatsappMessage += `CPF: ${formData.cpf}\n`;
            whatsappMessage += `Telefone: ${formData.phone}\n`;
            whatsappMessage += `Endereço: ${formData.address}\n`;
            whatsappMessage += `CEP: ${formData.cep}\n`;
            whatsappMessage += `@ de Rede Social: ${formData.socialMedia}\n\n`;
            whatsappMessage += `*Arquivos Anexados (Nomes de Arquivo para Referência):*\n`;
            whatsappMessage += `RG ou CNH: ${formData.rgCnh}\n`;
            whatsappMessage += `Comprovante de Residência: ${formData.proofOfResidence}\n`;
            whatsappMessage += `Selfie com Documento: ${formData.selfieWithDoc}\n`;
            whatsappMessage += `Print do Perfil de Rede Social: ${formData.socialMediaPrint}\n\n`;
            whatsappMessage += `*Para acelerar o processo de análise, por favor, envie os arquivos (RG/CNH, Comprovante de Residência, Selfie com Documento e Print do Perfil de Rede Social) diretamente por aqui no WhatsApp. Agradecemos a sua colaboração!*`;


            // Número de telefone do WhatsApp (incluindo código do país e DDD, sem sinais como +, -, espaços)
            const whatsappNumber = '5548999541113'; // +55 48 99954-1113

            // Codificar a mensagem para URL
            const encodedMessage = encodeURIComponent(whatsappMessage);

            // Criar o link do WhatsApp
            const whatsappLink = `https://wa.me/${whatsappNumber}?text=${encodedMessage}`;

            // Abrir o link em uma nova aba
            window.open(whatsappLink, '_blank');

            // Fechar o pop-up do formulário
            closePopup('registrationFormPopup');
            // Opcionalmente, limpa o formulário
            this.reset();
        });
    </script>

</body>
</html>
�
