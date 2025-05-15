<html lang="en">
<head>
  <title>Dream Tracker</title>
  <link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>✨</text></svg>">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }
    
    body {
      background-color: black;
      color: white;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 2.5rem 1rem;
    }
    
    h1 {
      font-size: 2.25rem;
      font-weight: bold;
      margin-bottom: 1rem;
      text-align: center;
    }
    
    .quote {
      font-size: 1.25rem;
      font-style: italic;
      margin-bottom: 3rem;
      text-align: center;
    }
    
    .qr-container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 2rem;
      margin-top: 2rem;
    }
    
    .qr-box {
      background-color: white;
      padding: 0.5rem;
      border-radius: 0.375rem;
      display: flex;
      flex-direction: column;
      box-shadow: 0 4px 6px rgba(255, 255, 255, 0.1);
      transition: transform 0.2s ease;
    }
    
    .qr-box:hover {
      transform: translateY(-5px);
    }
    
    .qr-img {
      width: 200px;
      height: 200px;
      object-fit: contain;
    }
    
    .address-container {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-top: 0.5rem;
      padding: 0.25rem 0.5rem;
      background-color: #f3f4f6;
      border-radius: 0.25rem;
      font-size: 0.75rem;
    }
    
    .address {
      color: black;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      max-width: 150px;
    }
    
    .copy-btn {
      margin-left: 0.25rem;
      padding: 0.25rem 0.5rem;
      background-color: black;
      color: white;
      border: none;
      border-radius: 0.25rem;
      cursor: pointer;
      font-size: 0.75rem;
      transition: background-color 0.2s ease;
    }
    
    .copy-btn:hover {
      background-color: #333;
    }
    
    .tagline {
      color: #22d3ee;
      font-size: 1.25rem;
      font-style: italic;
      margin: 2.5rem 0;
      max-width: 42rem;
      text-align: center;
    }
    
    .contact-box {
      display: flex;
      align-items: center;
      background-color: white;
      padding: 0.5rem 1rem;
      border-radius: 0.375rem;
      margin-top: 1rem;
      box-shadow: 0 4px 6px rgba(255, 255, 255, 0.1);
      transition: transform 0.2s ease;
    }
    
    .contact-box:hover {
      transform: translateY(-2px);
    }
    
    .contact-icon {
      color: black;
      margin-right: 0.5rem;
    }
    
    .contact-text {
      color: black;
    }
    
    .contact-link {
      color: black;
      text-decoration: none;
      transition: color 0.2s ease;
    }
    
    .contact-link:hover {
      color: #2563eb;
      text-decoration: underline;
    }
    
    .toast {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background-color: #22d3ee;
      color: black;
      padding: 10px 20px;
      border-radius: 4px;
      opacity: 0;
      transition: opacity 0.3s ease;
      pointer-events: none;
    }
    
    .toast.show {
      opacity: 1;
    }
    
    @media (max-width: 768px) {
      h1 {
        font-size: 1.75rem;
      }
      
      .quote, .tagline {
        font-size: 1rem;
      }
      
      .qr-container {
        gap: 1rem;
      }
      
      .qr-img {
        width: 150px;
        height: 150px;
      }
    }
  </style>
</head>
<body>
  <h1>Dream Tracker</h1>
  <p class="quote">"I want to buy my mom a house."</p>
  
  <div class="qr-container">
    <div class="qr-box">
      <img src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/solana_address_qr-fTcPZr2o32mdiGvFQ5T4SbiUl1Ri7Y.png" alt="Bitcoin QR Code" class="qr-img">
      <div class="address-container">
        <span class="address">bc1pyvlw67ewr8pvx22y25tgt5emwrcffmvtqpnajqpatp6xzzxsdawssccsgz</span>
        <button class="copy-btn" onclick="copyToClipboard('bc1pyvlw67ewr8pvx22y25tgt5emwrcffmvtqpnajqpatp6xzzxsdawssccsgz')">Copy</button>
      </div>
    </div>
    
    <div class="qr-box">
      <img src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/sol-KeLIZHrlVe4CaB86AUITBsZfCX1TUx.jpeg" alt="Solana QR Code" class="qr-img">
      <div class="address-container">
        <span class="address">D6ToiB3DQudsUcvYso8S9wywyMovBsGuKGCLegt6d3cg</span>
        <button class="copy-btn" onclick="copyToClipboard('D6ToiB3DQudsUcvYso8S9wywyMovBsGuKGCLegt6d3cg')">Copy</button>
      </div>
    </div>
    
    <div class="qr-box">
      <img src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/ethe-gIFifAkyy883qaNzE6EEcAFRFlHMAc.jpeg" alt="Ethereum QR Code" class="qr-img">
      <div class="address-container">
        <span class="address">0x77AB40f0F201Df968ba9102D685e49DA12397aBD</span>
        <button class="copy-btn" onclick="copyToClipboard('0x77AB40f0F201Df968ba9102D685e49DA12397aBD')">Copy</button>
      </div>
    </div>
  </div>
  
  <p class="tagline">"Share your dreams with us — and let's turn them into reality."</p>
  
  <div class="contact-box">
    <svg class="contact-icon" xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
      <rect x="2" y="4" width="20" height="16" rx="2"></rect>
      <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"></path>
    </svg>
    <span class="contact-text">info.dreamtracker@gmail.com</span>
    <button class="copy-btn" style="margin-left: 1rem;" onclick="copyToClipboard('info.dreamtracker@gmail.com')">Copy</button>
  </div>
  
  <div class="contact-box">
    <svg class="contact-icon" xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
      <path d="M9 12a3 3 0 1 0 6 0a3 3 0 0 0 -6 0"></path>
      <path d="M16.5 7.5v.001"></path>
      <path d="M20.5 4.5l-17 0c-1.5 0 -3 1.5 -3 3l0 9c0 1.5 1.5 3 3 3l17 0c1.5 0 3 -1.5 3 -3l0 -9c0 -1.5 -1.5 -3 -3 -3"></path>
    </svg>
    <a href="https://www.tiktok.com/@dream.tracker" target="_blank" rel="noopener noreferrer" class="contact-link">dream.tracker</a>
  </div>
  
  <div id="toast" class="toast">Copied to clipboard!</div>
  
  <script>
    function copyToClipboard(text) {
      navigator.clipboard.writeText(text)
        .then(() => {
          const toast = document.getElementById('toast');
          toast.classList.add('show');
          setTimeout(() => {
            toast.classList.remove('show');
          }, 2000);
        })
        .catch(err => {
          console.error('Failed to copy: ', err);
          alert("Failed to copy. Please try again.");
        });
    }
    
    // Preload images to ensure they display properly
    window.addEventListener('load', function() {
      const images = [
        'https://hebbkx1anhila5yf.public.blob.vercel-storage.com/solana_address_qr-fTcPZr2o32mdiGvFQ5T4SbiUl1Ri7Y.png',
        'https://hebbkx1anhila5yf.public.blob.vercel-storage.com/sol-KeLIZHrlVe4CaB86AUITBsZfCX1TUx.jpeg',
        'https://hebbkx1anhila5yf.public.blob.vercel-storage.com/ethe-gIFifAkyy883qaNzE6EEcAFRFlHMAc.jpeg'
      ];
      
      images.forEach(src => {
        const img = new Image();
        img.src = src;
      });
    });
  </script>
</body>
</html>
