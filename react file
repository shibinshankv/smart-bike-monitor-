```react
import React, { useState, useEffect } from 'react';
import { 
  Bike, 
  BatteryCharging, 
  AlertTriangle, 
  Power, 
  Clock, 
  ShieldCheck, 
  X,
  Info
} from 'lucide-react';

export default function App() {
  // --- State Management ---
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [isFirstLaunch, setIsFirstLaunch] = useState(true);
  
  // Hardware Simulation States
  const [batteryOn, setBatteryOn] = useState(false);
  const [standOn, setStandOn] = useState(false);
  const [activeTimeSeconds, setActiveTimeSeconds] = useState(0);

  // --- Timer Logic ---
  useEffect(() => {
    let interval = null;
    
    // If BOTH battery is on and stand is down, start counting
    if (batteryOn && standOn) {
      interval = setInterval(() => {
        setActiveTimeSeconds((prev) => prev + 1);
      }, 1000);
    } else {
      // Reset timer if either condition is no longer met
      if (interval) clearInterval(interval);
      setActiveTimeSeconds(0);
    }

    return () => {
      if (interval) clearInterval(interval);
    };
  }, [batteryOn, standOn]);

  // --- Helper Functions ---
  const formatTime = (totalSeconds) => {
    const minutes = Math.floor(totalSeconds / 60);
    const seconds = totalSeconds % 60;
    return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
  };

  const handleLogin = (e) => {
    e.preventDefault();
    setIsLoggedIn(true);
  };

  const isWastingBattery = batteryOn && standOn;

  return (
    <div className="min-h-screen bg-gray-950 flex items-center justify-center p-4 font-sans selection:bg-emerald-500/30">
      {/* Mobile Device Mockup Container */}
      <div className="relative w-full max-w-[390px] h-[844px] max-h-[95vh] bg-gray-900 rounded-[3rem] ring-8 ring-gray-800 shadow-2xl overflow-hidden flex flex-col">
        
        {/* Device Notch / Status Bar Area */}
        <div className="absolute top-0 inset-x-0 h-7 flex justify-center z-50">
          <div className="w-32 h-6 bg-gray-800 rounded-b-3xl"></div>
        </div>

        {/* Dynamic Screens */}
        {!isLoggedIn ? (
          // --- REGISTRATION SCREEN ---
          <div className="flex-1 flex flex-col p-6 pt-16 animate-in fade-in zoom-in-95 duration-500">
            <div className="flex-1 flex flex-col justify-center">
              <div className="w-16 h-16 bg-emerald-500/20 text-emerald-400 rounded-2xl flex items-center justify-center mb-6 border border-emerald-500/30 shadow-[0_0_15px_rgba(16,185,129,0.2)]">
                <Bike size={32} />
              </div>
              <h1 className="text-3xl font-bold text-white mb-2">Register Bike</h1>
              <p className="text-gray-400 text-sm mb-8">
                Connect your IoT accessory to start monitoring your motorcycle's battery status.
              </p>

              <form onSubmit={handleLogin} className="space-y-4">
                <div>
                  <label className="block text-xs font-medium text-gray-400 mb-1">Email Address</label>
                  <input 
                    type="email" 
                    required
                    placeholder="rider@example.com"
                    className="w-full bg-gray-800 border border-gray-700 text-white rounded-xl px-4 py-3 focus:outline-none focus:ring-2 focus:ring-emerald-500 transition-all placeholder:text-gray-600"
                  />
                </div>
                <div>
                  <label className="block text-xs font-medium text-gray-400 mb-1">Bike Register Number</label>
                  <input 
                    type="text" 
                    required
                    placeholder="KL-11-AB-1234"
                    className="w-full bg-gray-800 border border-gray-700 text-white rounded-xl px-4 py-3 focus:outline-none focus:ring-2 focus:ring-emerald-500 transition-all placeholder:text-gray-600 uppercase"
                  />
                </div>
                <div>
                  <label className="block text-xs font-medium text-gray-400 mb-1">Engine Chassis Number</label>
                  <input 
                    type="text" 
                    required
                    placeholder="ME3U3S5C1C2..."
                    className="w-full bg-gray-800 border border-gray-700 text-white rounded-xl px-4 py-3 focus:outline-none focus:ring-2 focus:ring-emerald-500 transition-all placeholder:text-gray-600 uppercase"
                  />
                </div>

                <button 
                  type="submit"
                  className="w-full bg-emerald-500 hover:bg-emerald-600 text-white font-semibold rounded-xl px-4 py-4 mt-4 transition-colors flex items-center justify-center gap-2 shadow-lg shadow-emerald-500/20"
                >
                  <ShieldCheck size={20} />
                  Connect Bike
                </button>
              </form>
            </div>
          </div>
        ) : (
          // --- HOME SCREEN ---
          <div className="flex-1 flex flex-col relative bg-black animate-in slide-in-from-right duration-300">
            
            {/* FIRST TIME USER MODAL */}
            {isFirstLaunch && (
              <div className="absolute inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-6 animate-in fade-in duration-300">
                <div className="bg-gray-800 border border-gray-700 p-6 rounded-3xl shadow-2xl relative max-w-sm w-full">
                  <button 
                    onClick={() => setIsFirstLaunch(false)}
                    className="absolute top-4 right-4 text-gray-400 hover:text-white"
                  >
                    <X size={20} />
                  </button>
                  <div className="w-12 h-12 bg-blue-500/20 text-blue-400 rounded-full flex items-center justify-center mb-4">
                    <Info size={24} />
                  </div>
                  <h3 className="text-xl font-bold text-white mb-2">Welcome!</h3>
                  <p className="text-gray-300 text-sm mb-6 leading-relaxed">
                    This dashboard shows your live battery status. If you leave your bike on the stand with the power running, we'll alert you here to prevent battery drain.
                  </p>
                  <button 
                    onClick={() => setIsFirstLaunch(false)}
                    className="w-full bg-white text-black font-semibold rounded-xl py-3 hover:bg-gray-200 transition-colors"
                  >
                    Got it
                  </button>
                </div>
              </div>
            )}

            {/* LIVE ALERT BANNER */}
            <div className={`transition-all duration-300 ease-in-out overflow-hidden ${isWastingBattery ? 'max-h-24 opacity-100' : 'max-h-0 opacity-0'}`}>
              <div className="bg-red-600 pt-10 pb-3 px-4 flex items-center justify-center gap-2 animate-pulse shadow-[0_4px_20px_rgba(220,38,38,0.4)] relative z-40">
                <AlertTriangle size={18} className="text-white" />
                <span className="text-white font-semibold text-sm">Your bike is on. Go and turn it off.</span>
              </div>
            </div>

            <div className="flex-1 overflow-y-auto pb-6 custom-scrollbar">
              {/* Bike Header Image */}
              <div className="relative h-64 w-full">
                <div className="absolute inset-0 bg-gradient-to-t from-black via-black/40 to-transparent z-10"></div>
                <img 
                  src="https://images.unsplash.com/photo-1558981403-c5f9899a28bc?w=800&q=80" 
                  alt="Motorcycle" 
                  className={`w-full h-full object-cover transition-transform duration-700 ${isWastingBattery ? 'scale-105 filter grayscale-[30%]' : ''}`}
                />
                <div className="absolute bottom-4 left-6 z-20">
                  <h2 className="text-3xl font-bold text-white drop-shadow-md">Royal Enfield</h2>
                  <p className="text-gray-300 font-medium">Classic 350</p>
                </div>
              </div>

              {/* Status Dashboard */}
              <div className="px-6 -mt-2 relative z-20">
                
                {/* Active Timer Card (Only shows when wasting battery) */}
                {isWastingBattery && (
                  <div className="bg-red-500/10 border border-red-500/30 rounded-2xl p-4 mb-4 flex items-center justify-between animate-in fade-in slide-in-from-top-4">
                    <div className="flex items-center gap-3">
                      <div className="w-10 h-10 bg-red-500/20 text-red-500 rounded-full flex items-center justify-center">
                        <Clock size={20} className="animate-spin-slow" style={{ animationDuration: '3s' }} />
                      </div>
                      <div>
                        <p className="text-red-400 text-xs font-semibold uppercase tracking-wider">Drain Time</p>
                        <p className="text-white font-mono text-xl">{formatTime(activeTimeSeconds)}</p>
                      </div>
                    </div>
                  </div>
                )}

                {/* Status Grid */}
                <div className="grid grid-cols-2 gap-4 mb-6">
                  {/* Battery Status */}
                  <div className={`p-4 rounded-2xl border transition-colors ${batteryOn ? 'bg-emerald-500/10 border-emerald-500/30' : 'bg-gray-800/50 border-gray-700'}`}>
                    <BatteryCharging size={24} className={`mb-2 ${batteryOn ? 'text-emerald-400' : 'text-gray-500'}`} />
                    <p className="text-gray-400 text-xs font-medium mb-1">Ignition/Battery</p>
                    <p className={`text-lg font-bold ${batteryOn ? 'text-emerald-400' : 'text-white'}`}>
                      {batteryOn ? 'ON' : 'OFF'}
                    </p>
                  </div>

                  {/* Stand Status */}
                  <div className={`p-4 rounded-2xl border transition-colors ${standOn ? 'bg-amber-500/10 border-amber-500/30' : 'bg-gray-800/50 border-gray-700'}`}>
                    <Power size={24} className={`mb-2 ${standOn ? 'text-amber-400' : 'text-gray-500'}`} />
                    <p className="text-gray-400 text-xs font-medium mb-1">Side Stand</p>
                    <p className={`text-lg font-bold ${standOn ? 'text-amber-400' : 'text-white'}`}>
                      {standOn ? 'ENGAGED' : 'UP'}
                    </p>
                  </div>
                </div>

                {/* --- HARDWARE SIMULATOR PANEL (For testing purposes) --- */}
                <div className="bg-gray-900 border border-gray-800 rounded-3xl p-5 shadow-inner">
                  <div className="flex items-center gap-2 mb-4">
                    <div className="w-2 h-2 rounded-full bg-blue-500 animate-pulse"></div>
                    <h3 className="text-sm font-semibold text-gray-300 uppercase tracking-wider">IoT Hardware Simulator</h3>
                  </div>
                  <p className="text-xs text-gray-500 mb-5">
                    Toggle these buttons to simulate incoming cellular data from the physical bike accessory.
                  </p>
                  
                  <div className="space-y-4">
                    <div className="flex items-center justify-between">
                      <span className="text-sm text-white font-medium">Ignition Sensor</span>
                      <button 
                        onClick={() => setBatteryOn(!batteryOn)}
                        className={`relative inline-flex h-7 w-14 items-center rounded-full transition-colors ${batteryOn ? 'bg-emerald-500' : 'bg-gray-700'}`}
                      >
                        <span className={`inline-block h-5 w-5 transform rounded-full bg-white transition-transform ${batteryOn ? 'translate-x-8' : 'translate-x-1'}`} />
                      </button>
                    </div>
                    
                    <div className="flex items-center justify-between">
                      <span className="text-sm text-white font-medium">Stand Sensor</span>
                      <button 
                        onClick={() => setStandOn(!standOn)}
                        className={`relative inline-flex h-7 w-14 items-center rounded-full transition-colors ${standOn ? 'bg-amber-500' : 'bg-gray-700'}`}
                      >
                        <span className={`inline-block h-5 w-5 transform rounded-full bg-white transition-transform ${standOn ? 'translate-x-8' : 'translate-x-1'}`} />
                      </button>
                    </div>
                  </div>
                </div>

              </div>
            </div>
          </div>
        )}
      </div>

      <style dangerouslySetInnerHTML={{__html: `
        .custom-scrollbar::-webkit-scrollbar {
          width: 0px;
          background: transparent;
        }
      `}} />
    </div>
  );
}
```