# Ultra
The AI chatbot that can help you accomplish anything!
import React, { useState, useEffect, useRef } from "react";

export default function UltraApp() {
  const [activeTab, setActiveTab] = useState("chat");
  const [sidebarOpen, setSidebarOpen] = useState(true);
  const [voiceMode, setVoiceMode] = useState(false);
  const [messages, setMessages] = useState([
    { role: "assistant", content: "Welcome to Ultra." }
  ]);
  const [input, setInput] = useState("");
  const [code, setCode] = useState("<h1>Hello from Ultra Code</h1>");
  const iframeRef = useRef(null);

  // Voice speak only if voice mode ON
  const speak = (text) => {
    if (!voiceMode) return;
    const utter = new SpeechSynthesisUtterance(text);
    speechSynthesis.speak(utter);
  };

  const sendMessage = () => {
    if (!input.trim()) return;
    const newMessages = [
      ...messages,
      { role: "user", content: input },
      { role: "assistant", content: "Ultra response placeholder." }
    ];
    setMessages(newMessages);
    speak("Ultra response placeholder.");
    setInput("");
  };

  const previewCode = () => {
    const iframe = iframeRef.current;
    iframe.srcdoc = code;
  };

  const backgrounds = {
    classic: ["#e3f2fd", "#f5f5dc"],
    modern: ["#121212", "#1f1f1f"],
    fun: ["#ffeb3b", "#ff4081"]
  };

  const [bgColor, setBgColor] = useState("#ffffff");

  return (
    <div style={{ display: "flex", height: "100vh", background: bgColor }}>
      
      {sidebarOpen && (
        <div style={{
          width: "250px",
          background: "#2e2e48",
          color: "white",
          padding: "15px",
          display: "flex",
          flexDirection: "column"
        }}>
          
          <div style={{ display: "flex", justifyContent: "space-between" }}>
            <div>
              <div style={{ fontSize: "24px" }}>U ⭐⭐⭐⭐⭐</div>
            </div>
            <button onClick={() => setSidebarOpen(false)}>✖</button>
          </div>

          <button onClick={() => setActiveTab("chat")}>Chat</button>
          <button onClick={() => setActiveTab("ultracode")}>Ultra Code</button>
          <button onClick={() => setActiveTab("library")}>Library</button>
          <button onClick={() => setActiveTab("doodle")}>Doodle Center</button>
          <button onClick={() => setActiveTab("settings")}>Settings</button>

        </div>
      )}

      {!sidebarOpen && (
        <button onClick={() => setSidebarOpen(true)}>☰</button>
      )}

      <div style={{ flex: 1, padding: "20px", overflow: "auto" }}>
        
        {activeTab === "chat" && (
          <div>
            <h2>Ultra Chat</h2>

            <label>
              <input
                type="checkbox"
                checked={voiceMode}
                onChange={() => setVoiceMode(!voiceMode)}
              />
              Voice Mode
            </label>

            <div style={{ height: "300px", overflowY: "auto", border: "1px solid #ccc", padding: "10px" }}>
              {messages.map((msg, i) => (
                <div key={i}>
                  <strong>{msg.role}:</strong> {msg.content}
                </div>
              ))}
            </div>

            <input
              value={input}
              onChange={(e) => setInput(e.target.value)}
              placeholder="Message Ultra..."
            />
            <button onClick={sendMessage}>Send</button>
          </div>
        )}

        {activeTab === "ultracode" && (
          <div>
            <h2>Ultra Code</h2>

            <textarea
              value={code}
              onChange={(e) => setCode(e.target.value)}
              style={{ width: "100%", height: "200px" }}
            />

            <div style={{ marginTop: "10px" }}>
              <button onClick={previewCode}>Preview</button>
              <button onClick={() => navigator.clipboard.writeText(code)}>Copy</button>
              <button
                onClick={() => {
                  const blob = new Blob([code], { type: "text/html" });
                  const link = document.createElement("a");
                  link.href = URL.createObjectURL(blob);
                  link.download = "ultra-code.html";
                  link.click();
                }}
              >
                Download
              </button>
            </div>

            <iframe
              ref={iframeRef}
              title="preview"
              style={{ width: "100%", height: "300px", marginTop: "20px", border: "1px solid #ccc" }}
            />
          </div>
        )}

        {activeTab === "settings" && (
          <div>
            <h2>Background Settings</h2>

            <h3>Classic</h3>
            {backgrounds.classic.map((color, i) => (
              <button key={i} onClick={() => setBgColor(color)} style={{ background: color, width: "50px", height: "50px", margin: "5px" }} />
            ))}

            <h3>Modern</h3>
            {backgrounds.modern.map((color, i) => (
              <button key={i} onClick={() => setBgColor(color)} style={{ background: color, width: "50px", height: "50px", margin: "5px" }} />
            ))}

            <h3>Fun</h3>
            {backgrounds.fun.map((color, i) => (
              <button key={i} onClick={() => setBgColor(color)} style={{ background: color, width: "50px", height: "50px", margin: "5px" }} />
            ))}
          </div>
        )}

        {activeTab === "library" && <h2>Library (Coming Soon)</h2>}
        {activeTab === "doodle" && <h2>Doodle Center (Coming Soon)</h2>}

      </div>
    </div>
  );
}
