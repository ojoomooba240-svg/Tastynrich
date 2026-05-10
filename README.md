<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TastynRich Gourmet | Direct Order</title>
    <style>
        :root {
            --primary-orange: #e67e22;
            --dark-bg: #1a1a1a;
            --text-white: #ffffff;
            --gray-light: #f8f9fa;
            --success-green: #27ae60;
        }

        body { font-family: 'Segoe UI', Roboto, sans-serif; margin: 0; padding: 0; background-color: var(--gray-light); color: #333; }
        
        header {
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('https://images.unsplash.com/photo-1513104890138-7c749659a591?auto=format&fit=crop&w=800&q=80');
            background-size: cover;
            background-position: center;
            color: white;
            text-align: center;
            padding: 60px 20px;
        }

        .container { max-width: 800px; margin: auto; padding: 20px; }

        .info-card {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            margin-top: -40px;
            text-align: center;
        }

        /* Menu */
        .menu-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 30px; }
        @media (max-width: 600px) { .menu-grid { grid-template-columns: 1fr; } }

        .menu-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            border-left: 5px solid var(--primary-orange);
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        /* Bank Details Box */
        .bank-details {
            background: #fff3e0;
            border: 2px dashed var(--primary-orange);
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            display: none; /* Hidden until item selected */
        }

        .bank-details h3 { margin-top: 0; color: #d35400; }

        .btn {
            background: var(--primary-orange);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            font-weight: bold;
            font-size: 1rem;
            margin-top: 10px;
        }

        .whatsapp-btn {
            background: var(--success-green);
        }

        input, textarea {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
        }
    </style>
</head>
<body>

<header>
    <h1>TastynRich Gourmet</h1>
    <p>Premium Pizza & Intercontinental Dishes</p>
</header>

<div class="container">
    <div class="info-card">
        <p>📍 WP25+5R5, Ilishan-Remo, Ogun State</p>
        <p>🕒 8:00 AM - 10:00 PM</p>
    </div>

    <h2>Select Your Meal</h2>
    <div class="menu-grid">
        <div class="menu-card">
            <h3>Chicken & Pepperoni</h3>
            <p>₦5,500</p>
            <button class="btn" onclick="showBank('Chicken & Pepperoni Pizza', 5500)">Select</button>
        </div>
        <div class="menu-card">
            <h3>Beef Pizza</h3>
            <p>₦5,000</p>
            <button class="btn" onclick="showBank('Beef Pizza', 5000)">Select</button>
        </div>
    </div>

    <div id="payment-section" class="bank-details">
        <h3>Step 1: Make Bank Transfer</h3>
        <p>Please pay <strong>₦<span id="price-tag"></span></strong> for <strong><span id="item-tag"></span></strong> to the account below:</p>
        
        <div style="background: white; padding: 15px; border-radius: 5px; margin-bottom: 15px;">
            <p><strong>Bank:</strong> [INSERT BANK NAME HERE]</p>
            <p><strong>Account Number:</strong> [INSERT ACCOUNT NUMBER]</p>
            <p><strong>Account Name:</strong> [INSERT ACCOUNT NAME]</p>
        </div>

        <h3>Step 2: Enter Delivery Details</h3>
        <input type="text" id="custName" placeholder="Your Name" required>
        <input type="text" id="custPhone" placeholder="Your Phone Number" required>
        <textarea id="custAddr" placeholder="Delivery Address in Ilishan-Remo" rows="3"></textarea>
        
        <button class="btn whatsapp-btn" onclick="sendToWhatsApp()">Confirm Payment & Order on WhatsApp</button>
        <p style="font-size: 0.8rem; color: #666; margin-top: 10px;">*You will be redirected to WhatsApp to send your transfer receipt.</p>
    </div>
</div>

<script>
    let selectedItem = "";
    let selectedPrice = 0;
    const RESTAURANT_WHATSAPP = "2348100245666"; // Business WhatsApp Number

    function showBank(item, price) {
        selectedItem = item;
        selectedPrice = price;
        document.getElementById('item-tag').innerText = item;
        document.getElementById('price-tag').innerText = price.toLocaleString();
        document.getElementById('payment-section').style.display = 'block';
        window.scrollTo({ top: document.getElementById('payment-section').offsetTop - 20, behavior: 'smooth' });
    }

    function sendToWhatsApp() {
        const name = document.getElementById('custName').value;
        const phone = document.getElementById('custPhone').value;
        const addr = document.getElementById('custAddr').value;

        if(!name || !phone || !addr) {
            alert("Please fill in all delivery details.");
            return;
        }

        const message = `*NEW ORDER - BANK TRANSFER*%0A%0A` +
                        `*Item:* ${selectedItem}%0A` +
                        `*Amount:* ₦${selectedPrice.toLocaleString()}%0A%0A` +
                        `*Customer Name:* ${name}%0A` +
                        `*Phone:* ${phone}%0A` +
                        `*Address:* ${addr}%0A%0A` +
                        `_I have made the transfer. I am sending the receipt now._`;

        const whatsappURL = `https://wa.me/${RESTAURANT_WHATSAPP}?text=${message}`;
        window.location.href = whatsappURL;
    }
</script>

</body>
</html>
