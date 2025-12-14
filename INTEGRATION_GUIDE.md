# Integration Guide: Adding Chatbot to Gandhamardan Agri Products Website

## Overview
This guide explains how to integrate the chatbot into the existing Gandhamardan Agri Products website (`index.html.html`).

## Method 1: Floating Chat Widget (Recommended)

Add this code before the closing `</body>` tag in your `index.html.html` file:

```html
<!-- Gandhamardan Agri Products Chatbot -->
<style>
.chatbot-container {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 1000;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.chatbot-toggle {
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, #3a7d44 0%, #2D5016 100%);
    border: none;
    border-radius: 50%;
    color: white;
    font-size: 24px;
    cursor: pointer;
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
}

.chatbot-toggle:hover {
    transform: scale(1.1);
}

.chatbot-window {
    width: 350px;
    height: 450px;
    background: white;
    border-radius: 10px;
    box-shadow: 0 5px 25px rgba(0,0,0,0.2);
    display: none;
    flex-direction: column;
    overflow: hidden;
    position: absolute;
    bottom: 70px;
    right: 0;
}

.chatbot-header {
    background: linear-gradient(135deg, #3a7d44 0%, #2D5016 100%);
    color: white;
    padding: 15px;
    text-align: center;
}

.chatbot-header h3 {
    margin: 0;
    font-size: 16px;
}

.chat-messages {
    flex: 1;
    padding: 15px;
    overflow-y: auto;
    background-color: #fafafa;
    height: 300px;
}

.message {
    margin-bottom: 10px;
    padding: 8px 12px;
    border-radius: 8px;
    max-width: 80%;
    font-size: 14px;
}

.bot-message {
    background-color: #e8f5e9;
    align-self: flex-start;
}

.user-message {
    background-color: #d1ecf1;
    margin-left: auto;
    text-align: right;
}

.input-area {
    display: flex;
    padding: 10px;
    background: white;
    border-top: 1px solid #eee;
}

#chatbot-input {
    flex: 1;
    padding: 8px 12px;
    border: 1px solid #ddd;
    border-radius: 15px;
    font-size: 14px;
    outline: none;
}

#chatbot-send {
    margin-left: 8px;
    padding: 8px 15px;
    background-color: #3a7d44;
    color: white;
    border: none;
    border-radius: 15px;
    cursor: pointer;
    font-size: 14px;
}

.welcome-message {
    text-align: center;
    padding: 10px;
    color: #666;
    font-style: italic;
    font-size: 14px;
}
</style>

<div class="chatbot-container">
    <button class="chatbot-toggle" id="chatbot-toggle">💬</button>
    <div class="chatbot-window" id="chatbot-window">
        <div class="chatbot-header">
            <h3>🌾 Gandhamardan Assistant</h3>
        </div>
        <div class="chat-messages" id="chatbot-messages">
            <div class="welcome-message">
                Hi! I'm your Gandhamardan Agri Products assistant. Ask about our organic products!
            </div>
            <div class="message bot-message">
                Hello! I can provide information about our organic rice, millet products, NutriBloom supplements, and traditional herbs. For pricing, please use Contact Us.
            </div>
        </div>
        <div class="input-area">
            <input type="text" id="chatbot-input" placeholder="Ask about our products..." autocomplete="off">
            <button id="chatbot-send">Send</button>
        </div>
    </div>
</div>

<script>
// Chatbot logic (simplified version for integration)
document.addEventListener('DOMContentLoaded', function() {
    const toggleBtn = document.getElementById('chatbot-toggle');
    const chatWindow = document.getElementById('chatbot-window');
    const chatInput = document.getElementById('chatbot-input');
    const chatMessages = document.getElementById('chatbot-messages');
    const sendBtn = document.getElementById('chatbot-send');
    
    // Toggle chat window
    toggleBtn.addEventListener('click', function() {
        chatWindow.style.display = chatWindow.style.display === 'flex' ? 'none' : 'flex';
        if (chatWindow.style.display === 'flex') {
            chatInput.focus();
        }
    });
    
    // Send message function
    function sendMessage() {
        const message = chatInput.value.trim();
        if (message === '') return;
        
        // Add user message
        addMessage(message, true);
        chatInput.value = '';
        
        // Generate bot response after a short delay
        setTimeout(() => {
            const response = generateBotResponse(message);
            addMessage(response, false);
        }, 500);
    }
    
    // Add message to chat
    function addMessage(text, isUser) {
        const messageDiv = document.createElement('div');
        messageDiv.className = `message ${isUser ? 'user-message' : 'bot-message'}`;
        messageDiv.textContent = text;
        chatMessages.appendChild(messageDiv);
        
        // Scroll to bottom
        chatMessages.scrollTop = chatMessages.scrollHeight;
    }
    
    // Simplified response generation
    function generateBotResponse(userMessage) {
        const msg = userMessage.toLowerCase();
        
        if (msg.includes('rice') || msg.includes('black') || msg.includes('red') || msg.includes('white')) {
            return "We offer various organic rice varieties including Black, Red, and White rice. For specific details about our rice products, I can provide more information. For pricing, please use our Contact Us section.";
        } else if (msg.includes('millet') || msg.includes('snack')) {
            return "Our millet products include packaged snacks, namkeen, murukku, and ready-to-eat cookies. These are gluten-free and traditionally processed. For pricing information, please contact us directly.";
        } else if (msg.includes('nutribloom') || msg.includes('protein')) {
            return "NutriBloom features super protein powder and natural nutrition supplements rich in antioxidants. For more details about our nutrition products, feel free to ask. For pricing, please use our Contact Us section.";
        } else if (msg.includes('herb') || msg.includes('ashwagandha') || msg.includes('triphala') || msg.includes('amla')) {
            return "We offer 48+ traditional Ayurvedic herbs available in raw and powder form. For specific herb information, I can provide details. For pricing, please contact us directly.";
        } else if (msg.includes('price') || msg.includes('cost') || msg.includes('buy') || msg.includes('order') || msg.includes('bulk') || msg.includes('wholesale')) {
            return "Pricing and commercial details are handled directly by our team. Please use the 'Contact Us' section of our website for product pricing, bulk orders, wholesale supply, or export enquiries.";
        } else if (msg.includes('hello') || msg.includes('hi')) {
            return "Hello! I'm the official virtual assistant for Gandhamardan Agri Products. I can provide information about our organic rice, millet products, NutriBloom supplements, and traditional herbs. For pricing, please use Contact Us.";
        } else {
            return "Thank you for your inquiry. I can provide detailed information about our organic products. For pricing information or commercial inquiries, please use the Contact Us section of our website.";
        }
    }
    
    // Event listeners
    sendBtn.addEventListener('click', sendMessage);
    
    chatInput.addEventListener('keypress', function(e) {
        if (e.key === 'Enter') {
            sendMessage();
        }
    });
});
</script>
```

## Method 2: Page Embed

Alternatively, you can link to the standalone chatbot page from your navigation:

Add this link to your website's navigation:
```html
<a href="chatbot.html" target="_blank">Chat with Assistant</a>
```

## Brand Color Matching

The chatbot uses your brand colors:
- Primary: #3a7d44 (green)
- Secondary: #2D5016 (dark green)
- Accent: #eab308 (yellow)

These are integrated throughout the chatbot interface to maintain visual consistency with your website.

## Testing

After integration:
1. Test all major product categories (rice, millet, nutribloom, herbs)
2. Verify pricing inquiries redirect to Contact Us
3. Check responsive behavior on mobile devices
4. Ensure the chatbot doesn't interfere with existing website functionality