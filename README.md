# Ultra
The AI chatbot that can help you accomplish anything!
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./styles/global.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
import { useState } from "react";
import Sidebar from "./components/Sidebar";
import Chat from "./components/Chat";
import UltraCode from "./components/UltraCode";
import Settings from "./components/Settings";

export default function App() {
  const [activeTab, setActiveTab] = useState("chat");
  const [sidebarOpen, setSidebarOpen] = useState(true);

  const renderTab = () => {
    switch (activeTab) {
      case "chat":
        return <Chat />;
      case "ultracode":
        return <UltraCode />;
      case "settings":
        return <Settings />;
      default:
        return <Chat />;
    }
  };

  return (
    <div className="app">
      {sidebarOpen && (
        <Sidebar
          activeTab={activeTab}
          setActiveTab={setActiveTab}
          closeSidebar={() => setSidebarOpen(false)}
        />
      )}

      {!sidebarOpen && (
        <button
          className="open-sidebar"
          onClick={() => setSidebarOpen(true)}
        >
          ☰
        </button>
      )}

      <div className="main-content">{renderTab()}</div>
    </div>
  );
}
import { useState } from "react";

export default function Chat() {
  const [messages, setMessages] = useState([
    { role: "assistant", content: "Welcome to Ultra." }
  ]);
  const [input, setInput] = useState("");
  const [voiceMode, setVoiceMode] = useState(false);

  const speak = (text) => {
    if (!voiceMode) return;
    const utter = new SpeechSynthesisUtterance(text);
    speechSynthesis.speak(utter);
  };

  const sendMessage = () => {
    if (!input.trim()) return;

    const reply = "Ultra response placeholder.";

    setMessages([
      ...messages,
      { role: "user", content: input },
      { role: "assistant", content: reply }
    ]);

    speak(reply);
    setInput("");
  };

  return (
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

      <div className="chat-box">
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
  );
}
import { useState } from "react";

export default function Chat() {
  const [messages, setMessages] = useState([
    { role: "assistant", content: "Welcome to Ultra." }
  ]);
  const [input, setInput] = useState("");
  const [voiceMode, setVoiceMode] = useState(false);

  const speak = (text) => {
    if (!voiceMode) return;
    const utter = new SpeechSynthesisUtterance(text);
    speechSynthesis.speak(utter);
  };

  const sendMessage = () => {
    if (!input.trim()) return;

    const reply = "Ultra response placeholder.";

    setMessages([
      ...messages,
      { role: "user", content: input },
      { role: "assistant", content: reply }
    ]);

    speak(reply);
    setInput("");
  };

  return (
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

      <div className="chat-box">
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
  );
}
import { useRef, useState } from "react";

export default function UltraCode() {
  const [code, setCode] = useState("<h1>Hello Ultra Code</h1>");
  const iframeRef = useRef(null);

  const preview = () => {
    iframeRef.current.srcdoc = code;
  };

  return (
    <div>
      <h2>Ultra Code</h2>

      <textarea
        className="code-editor"
        value={code}
        onChange={(e) => setCode(e.target.value)}
      />

      <div className="code-buttons">
        <button onClick={preview}>Preview</button>
        <button onClick={() => navigator.clipboard.writeText(code)}>
          Copy
        </button>
      </div>

      <iframe
        ref={iframeRef}
        className="preview-frame"
        title="preview"
      />
    </div>
  );
}
import { useState } from "react";

export default function Settings() {
  const [bg, setBg] = useState("#ffffff");

  return (
    <div style={{ background: bg, height: "100%" }}>
      <h2>Background Settings</h2>

      <button onClick={() => setBg("#e3f2fd")}>Classic Blue</button>
      <button onClick={() => setBg("#121212")}>Modern Dark</button>
      <button onClick={() => setBg("#ff4081")}>Fun Pink</button>
    </div>
  );
}
import { useState } from "react";

export default function Settings() {
  const [bg, setBg] = useState("#ffffff");

  return (
    <div style={{ background: bg, height: "100%" }}>
      <h2>Background Settings</h2>

      <button onClick={() => setBg("#e3f2fd")}>Classic Blue</button>
      <button onClick={() => setBg("#121212")}>Modern Dark</button>
      <button onClick={() => setBg("#ff4081")}>Fun Pink</button>
    </div>
  );
}
body {
  margin: 0;
  font-family: Arial, sans-serif;
}

.app {
  display: flex;
  height: 100vh;
}

.sidebar {
  width: 250px;
  background: #2e2e48;
  color: white;
  padding: 15px;
  display: flex;
  flex-direction: column;
}

.sidebar button {
  margin-top: 10px;
}

.sidebar .active {
  background: #444;
}

.main-content {
  flex: 1;
  padding: 20px;
  overflow: auto;
}

.chat-box {
  height: 250px;
  border: 1px solid #ccc;
  padding: 10px;
  overflow-y: auto;
}

.code-editor {
  width: 100%;
  height: 200px;
}

.preview-frame {
  width: 100%;
  height: 300px;
  border: 1px solid #ccc;
  margin-top: 10px;
}
body {
  margin: 0;
  font-family: Arial, sans-serif;
}

.app {
  display: flex;
  height: 100vh;
}

.sidebar {
  width: 250px;
  background: #2e2e48;
  color: white;
  padding: 15px;
  display: flex;
  flex-direction: column;
}

.sidebar button {
  margin-top: 10px;
}

.sidebar .active {
  background: #444;
}

.main-content {
  flex: 1;
  padding: 20px;
  overflow: auto;
}

.chat-box {
  height: 250px;
  border: 1px solid #ccc;
  padding: 10px;
  overflow-y: auto;
}

.code-editor {
  width: 100%;
  height: 200px;
}

.preview-frame {
  width: 100%;
  height: 300px;
  border: 1px solid #ccc;
  margin-top: 10px;
}
import { createContext, useContext, useEffect, useState } from "react";

const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    const storedUser = localStorage.getItem("ultra_user");
    if (storedUser) {
      setUser(JSON.parse(storedUser));
    }
  }, []);

  const signup = ({ email, password, age, region }) => {
    if (age < 10) {
      alert("You must be at least 10 years old to create an account.");
      return false;
    }

    const newUser = { email, password, age, region };
    localStorage.setItem("ultra_user", JSON.stringify(newUser));
    setUser(newUser);
    return true;
  };

  const login = ({ email, password }) => {
    const storedUser = JSON.parse(localStorage.getItem("ultra_user"));
    if (!storedUser) {
      alert("No account found.");
      return false;
    }

    if (storedUser.email === email && storedUser.password === password) {
      setUser(storedUser);
      return true;
    }

    alert("Invalid credentials.");
    return false;
  };

  const logout = () => {
    localStorage.removeItem("ultra_user");
    setUser(null);
  };

  return (
    <AuthContext.Provider value={{ user, signup, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export const useAuth = () => useContext(AuthContext);
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { AuthProvider } from "./context/AuthContext";
import { ThemeProvider } from "./context/ThemeContext";
import "./styles/global.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <AuthProvider>
      <ThemeProvider>
        <App />
      </ThemeProvider>
    </AuthProvider>
  </React.StrictMode>
);
import { useAuth } from "../context/AuthContext";
import { useTheme } from "../context/ThemeContext";

export default function Settings() {
  const { user } = useAuth();
  const { theme, toggleTheme } = useTheme();

  return (
    <div>
      <h2>Settings</h2>

      <button onClick={toggleTheme}>
        Switch to {theme === "light" ? "Dark" : "Light"} Mode
      </button>

      <h3>Background Customization</h3>

      {!user && <p>(Account required to change backgrounds)</p>}

      {user && (
        <>
          <button style={{ background: "#e3f2fd" }}>Classic Blue</button>
          <button style={{ background: "#121212", color: "white" }}>
            Modern Dark
          </button>
          <button style={{ background: "#ff4081" }}>Fun Pink</button>
        </>
      )}
    </div>
  );
}
body.light {
  background: #ffffff;
  color: #000;
}

body.dark {
  background: #121212;
  color: #ffffff;
}
body.light {
  background: #ffffff;
  color: #000;
}

body.dark {
  background: #121212;
  color: #ffffff;
}
export const saveToLibrary = (item) => {
  const existing = JSON.parse(localStorage.getItem("ultra_library")) || [];
  const updated = [...existing, item];
  localStorage.setItem("ultra_library", JSON.stringify(updated));
};

export const getLibrary = () => {
  return JSON.parse(localStorage.getItem("ultra_library")) || [];
};

export const deleteFromLibrary = (index) => {
  const existing = JSON.parse(localStorage.getItem("ultra_library")) || [];
  existing.splice(index, 1);
  localStorage.setItem("ultra_library", JSON.stringify(existing));
};
import { useState } from "react";
import { saveToLibrary } from "../utils/storage";
import { useAuth } from "../context/AuthContext";

export default function ImageGenerator() {
  const { user } = useAuth();
  const [prompt, setPrompt] = useState("");
  const [image, setImage] = useState(null);

  if (!user) {
    return <p>Account required to generate images.</p>;
  }

  const generate = () => {
    const canvas = document.createElement("canvas");
    canvas.width = 400;
    canvas.height = 300;
    const ctx = canvas.getContext("2d");

    ctx.fillStyle = "#" + Math.floor(Math.random()*16777215).toString(16);
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    ctx.fillStyle = "white";
    ctx.font = "20px Arial";
    ctx.fillText(prompt, 20, 150);

    const data = canvas.toDataURL();
    setImage(data);
  };

  const save = () => {
    saveToLibrary({ type: "image", data: image });
    alert("Saved to Library!");
  };

  return (
    <div>
      <h2>Ultra Image Engine (Beta)</h2>

      <input
        placeholder="Describe your image..."
        value={prompt}
        onChange={(e) => setPrompt(e.target.value)}
      />

      <button onClick={generate}>Generate</button>

      {image && (
        <>
          <img src={image} alt="generated" width="300" />
          <button onClick={save}>Save to Library</button>
        </>
      )}
    </div>
  );
}
case "library":
  return <Library />;
case "doodle":
  return <DoodleCenter />;
case "image":
  return <ImageGenerator />;
  case "library":
  return <Library />;
case "doodle":
  return <DoodleCenter />;
case "image":
  return <ImageGenerator />;
  import { useRef, useState } from "react";

export default function UltraCodePro() {
  const [code, setCode] = useState("<h1>Hello Ultra Code Pro</h1>");
  const iframeRef = useRef(null);

  const preview = () => {
    iframeRef.current.srcdoc = code;
  };

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: "10px" }}>
      <h2>Ultra Code Pro</h2>
      <textarea
        style={{ width: "100%", height: "200px" }}
        value={code}
        onChange={(e) => setCode(e.target.value)}
      />
      <div style={{ display: "flex", gap: "10px" }}>
        <button onClick={preview}>Preview</button>
        <button onClick={() => navigator.clipboard.writeText(code)}>Copy</button>
      </div>
      <iframe
        ref={iframeRef}
        style={{ width: "100%", height: "300px", border: "1px solid #ccc" }}
        title="preview"
      />
    </div>
  );
}
import { useAuth } from "../context/AuthContext";

export default function ShareButton({ content }) {
  const { user } = useAuth();

  if (!user) return null;

  const share = () => {
    const url = "https://ultra.fake.app/share?content=" + encodeURIComponent(content);
    prompt("Copy this link to share:", url);
  };

  return <button onClick={share}>Share ⬆</button>;
}
import { useState } from "react";
import { useAuth } from "../context/AuthContext";

export default function TeachUltra() {
  const { user } = useAuth();
  const [examples, setExamples] = useState([]);
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");

  if (!user) return <p>Account required to teach Ultra.</p>;

  const teach = () => {
    setExamples([...examples, { prompt, response }]);
    setPrompt("");
    setResponse("");
  };

  return (
    <div>
      <h2>Teach Ultra</h2>
      <input
        placeholder="Example prompt"
        value={prompt}
        onChange={(e) => setPrompt(e.target.value)}
      />
      <input
        placeholder="Expected response"
        value={response}
        onChange={(e) => setResponse(e.target.value)}
      />
      <button onClick={teach}>Add Example</button>

      <h3>Saved Examples</h3>
      {examples.map((e, i) => (
        <div key={i}>
          <strong>Prompt:</strong> {e.prompt} <br />
          <strong>Response:</strong> {e.response}
        </div>
      ))}
    </div>
  );
}
import { useState } from "react";
import { useAuth } from "../context/AuthContext";

export default function TeachUltra() {
  const { user } = useAuth();
  const [examples, setExamples] = useState([]);
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");

  if (!user) return <p>Account required to teach Ultra.</p>;

  const teach = () => {
    setExamples([...examples, { prompt, response }]);
    setPrompt("");
    setResponse("");
  };

  return (
    <div>
      <h2>Teach Ultra</h2>
      <input
        placeholder="Example prompt"
        value={prompt}
        onChange={(e) => setPrompt(e.target.value)}
      />
      <input
        placeholder="Expected response"
        value={response}
        onChange={(e) => setResponse(e.target.value)}
      />
      <button onClick={teach}>Add Example</button>

      <h3>Saved Examples</h3>
      {examples.map((e, i) => (
        <div key={i}>
          <strong>Prompt:</strong> {e.prompt} <br />
          <strong>Response:</strong> {e.response}
        </div>
      ))}
    </div>
  );
}
import { createContext, useContext, useEffect, useState } from "react";

const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  useEffect(() => {
    const saved = localStorage.getItem("ultra_theme");
    if (saved) setTheme(saved);
  }, []);

  useEffect(() => {
    localStorage.setItem("ultra_theme", theme);
    document.body.className = theme;
  }, [theme]);

  const toggleTheme = () => setTheme(theme === "light" ? "dark" : "light");

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export const useTheme = () => useContext(ThemeContext);
export const saveToLibrary = (item) => {
  const existing = JSON.parse(localStorage.getItem("ultra_library")) || [];
  localStorage.setItem("ultra_library", JSON.stringify([...existing, item]));
};

export const getLibrary = () => JSON.parse(localStorage.getItem("ultra_library")) || [];

export const deleteFromLibrary = (index) => {
  const existing = JSON.parse(localStorage.getItem("ultra_library")) || [];
  existing.splice(index, 1);
  localStorage.setItem("ultra_library", JSON.stringify(existing));
};
import { useState } from "react";
import AuthPanel from "./components/AuthPanel";
import Settings from "./components/Settings";
import Library from "./components/Library";
import DoodleCenter from "./components/DoodleCenter";
import ImageGenerator from "./components/ImageGenerator";
import UltraCodePro from "./components/UltraCodePro";
import GroupChat from "./components/GroupChat";
import ShareButton from "./components/ShareButton";
import TeachUltra from "./components/TeachUltra";
import { useAuth } from "./context/AuthContext";

export default function App() {
  const { user } = useAuth();
  const [activeTab, setActiveTab] = useState("chat");

  return (
    <div style={{ display: "flex", height: "100vh" }}>
      <aside style={{ width: 250, borderRight: "1px solid #ccc", padding: 10 }}>
        <h1>Ultra ★★★★★</h1>
        <button onClick={() => setActiveTab("chat")}>Chat</button>
        <button onClick={() => setActiveTab("library")}>Library</button>
        <button onClick={() => setActiveTab("doodle")}>Doodle Center</button>
        <button onClick={() => setActiveTab("image")}>Image Generator</button>
        <button onClick={() => setActiveTab("code")}>Ultra Code</button>
        <button onClick={() => setActiveTab("group")}>Group Chat</button>
        <button onClick={() => setActiveTab("teach")}>Teach Ultra</button>
        <Settings />
      </aside>
      <main style={{ flex: 1, padding: 10, overflowY: "auto" }}>
        {!user && <AuthPanel />}
        {activeTab === "chat" && <div>Chat UI placeholder</div>}
        {activeTab === "library" && <Library />}
        {activeTab === "doodle" && <DoodleCenter />}
        {activeTab === "image" && <ImageGenerator />}
        {activeTab === "code" && <UltraCodePro />}
        {activeTab === "group" && <GroupChat />}
        {activeTab === "teach" && <TeachUltra />}
      </main>
    </div>
  );
}
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { AuthProvider } from "./context/AuthContext";
import { ThemeProvider } from "./context/ThemeContext";
import "./styles/global.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <AuthProvider>
      <ThemeProvider>
        <App />
      </ThemeProvider>
    </AuthProvider>
  </React.StrictMode>
);
body.light { background: #fff; color: #000; }
body.dark { background: #121212; color: #fff; }
button { padding: 5px 10px; margin: 3px; cursor: pointer; }
textarea { font-family: monospace; }
body.light { background: #fff; color: #000; }
body.dark { background: #121212; color: #fff; }
button { padding: 5px 10px; margin: 3px; cursor: pointer; }
textarea { font-family: monospace; }
import { useState } from "react";
import { useAuth } from "../context/AuthContext";
import { CLASSIC_BACKGROUNDS, MODERN_BACKGROUNDS, FUN_BACKGROUNDS } from "../utils/backgrounds";

export default function Settings() {
  const { user } = useAuth();
  const [bg, setBg] = useState(localStorage.getItem("ultra_bg") || "");

  const applyBg = (color) => {
    setBg(color);
    localStorage.setItem("ultra_bg", color);
    document.body.style.background = color;
  };

  if (!user) return <p>Sign up to personalize backgrounds.</p>;

  return (
    <div>
      <h2>Backgrounds (Account Only)</h2>

      <h3>Classic</h3>
      {CLASSIC_BACKGROUNDS.map((b, i) => (
        <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>
          {b.name}
        </button>
      ))}

      <h3>Modern</h3>
      {MODERN_BACKGROUNDS.map((b, i) => (
        <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>
          {b.name}
        </button>
      ))}

      <h3>Fun</h3>
      {FUN_BACKGROUNDS.map((b, i) => (
        <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>
          {b.name}
        </button>
      ))}

      <button onClick={() => applyBg("")}>Reset Background</button>
    </div>
  );
}
import { useState } from "react";
import { useAuth } from "../context/AuthContext";
import { CLASSIC_BACKGROUNDS, MODERN_BACKGROUNDS, FUN_BACKGROUNDS } from "../utils/backgrounds";

export default function Settings() {
  const { user } = useAuth();
  const [bg, setBg] = useState(localStorage.getItem("ultra_bg") || "");

  const applyBg = (color) => {
    setBg(color);
    localStorage.setItem("ultra_bg", color);
    document.body.style.background = color;
  };

  if (!user) return <p>Sign up to personalize backgrounds.</p>;

  return (
    <div>
      <h2>Backgrounds (Account Only)</h2>

      <h3>Classic</h3>
      {CLASSIC_BACKGROUNDS.map((b, i) => (
        <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>
          {b.name}
        </button>
      ))}

      <h3>Modern</h3>
      {MODERN_BACKGROUNDS.map((b, i) => (
        <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>
          {b.name}
        </button>
      ))}

      <h3>Fun</h3>
      {FUN_BACKGROUNDS.map((b, i) => (
        <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>
          {b.name}
        </button>
      ))}

      <button onClick={() => applyBg("")}>Reset Background</button>
    </div>
  );
}
import { createContext, useContext, useEffect, useState } from "react";

const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    const storedUser = localStorage.getItem("ultra_user");
    if (storedUser) setUser(JSON.parse(storedUser));
  }, []);

  const signup = ({ email, password, age, region }) => {
    if (age < 10) { alert("You must be at least 10 years old."); return false; }
    const newUser = { email, password, age, region };
    localStorage.setItem("ultra_user", JSON.stringify(newUser));
    setUser(newUser);
    return true;
  };

  const login = ({ email, password }) => {
    const stored = JSON.parse(localStorage.getItem("ultra_user"));
    if (!stored) { alert("No account found"); return false; }
    if (stored.email === email && stored.password === password) { setUser(stored); return true; }
    alert("Invalid credentials"); return false;
  };

  const logout = () => { localStorage.removeItem("ultra_user"); setUser(null); };

  return <AuthContext.Provider value={{ user, signup, login, logout }}>{children}</AuthContext.Provider>;
}

export const useAuth = () => useContext(AuthContext);
export const saveToLibrary = (item) => {
  const existing = JSON.parse(localStorage.getItem("ultra_library")) || [];
  localStorage.setItem("ultra_library", JSON.stringify([...existing, item]));
};
export const getLibrary = () => JSON.parse(localStorage.getItem("ultra_library")) || [];
export const deleteFromLibrary = (index) => {
  const existing = JSON.parse(localStorage.getItem("ultra_library")) || [];
  existing.splice(index, 1);
  localStorage.setItem("ultra_library", JSON.stringify(existing));
};
import { useState } from "react";
import { useAuth } from "../context/AuthContext";
import { CLASSIC_BACKGROUNDS, MODERN_BACKGROUNDS, FUN_BACKGROUNDS } from "../utils/backgrounds";
import { useTheme } from "../context/ThemeContext";

export default function Settings() {
  const { user } = useAuth();
  const { theme, toggleTheme } = useTheme();
  const [bg, setBg] = useState(localStorage.getItem("ultra_bg") || "");

  const applyBg = (color) => {
    setBg(color);
    localStorage.setItem("ultra_bg", color);
    document.body.style.background = color;
  };

  if (!user) return <p>Sign up to personalize backgrounds.</p>;

  return (
    <div>
      <h2>Settings</h2>
      <button onClick={toggleTheme}>Toggle Theme ({theme})</button>

      <h3>Classic</h3>
      {CLASSIC_BACKGROUNDS.map((b, i) => <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>{b.name}</button>)}

      <h3>Modern</h3>
      {MODERN_BACKGROUNDS.map((b, i) => <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>{b.name}</button>)}

      <h3>Fun</h3>
      {FUN_BACKGROUNDS.map((b, i) => <button key={i} style={{ background: b.color, margin: "2px", padding: "5px" }} onClick={() => applyBg(b.color)}>{b.name}</button>)}

      <button onClick={() => applyBg("")}>Reset Background</button>
    </div>
  );
}
import { useState } from "react";
import { useAuth } from "./context/AuthContext";
import AuthPanel from "./components/AuthPanel";
import Settings from "./components/Settings";
import Library from "./components/Library";
import DoodleCenter from "./components/DoodleCenter";
import ImageGenerator from "./components/ImageGenerator";
import UltraCodePro from "./components/UltraCodePro";
import GroupChat from "./components/GroupChat";
import ShareButton from "./components/ShareButton";
import TeachUltra from "./components/TeachUltra";

export default function App() {
  const { user } = useAuth();
  const [activeTab, setActiveTab] = useState("chat");

  return (
    <div style={{ display: "flex", height: "100vh" }}>
      <aside style={{ width: 250, borderRight: "1px solid #ccc", padding: 10 }}>
        <h1>Ultra ★★★★★</h1>
        <button onClick={() => setActiveTab("chat")}>Chat</button>
        <button onClick={() => setActiveTab("library")}>Library</button>
        <button onClick={() => setActiveTab("doodle")}>Doodle Center</button>
        <button onClick={() => setActiveTab("image")}>Image Generator</button>
        <button onClick={() => setActiveTab("code")}>Ultra Code</button>
        <button onClick={() => setActiveTab("group")}>Group Chat</button>
        <button onClick={() => setActiveTab("teach")}>Teach Ultra</button>
        <Settings />
      </aside>
      <main style={{ flex: 1, padding: 10, overflowY: "auto" }}>
        {!user && <AuthPanel />}
        {activeTab === "chat" && <div>Chat UI placeholder</div>}
        {activeTab === "library" && <Library />}
        {activeTab === "doodle" && <DoodleCenter />}
        {activeTab === "image" && <ImageGenerator />}
        {activeTab === "code" && <UltraCodePro />}
        {activeTab === "group" && <GroupChat />}
        {activeTab === "teach" && <TeachUltra />}
      </main>
    </div>
  );
}
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { AuthProvider } from "./context/AuthContext";
import { ThemeProvider } from "./context/ThemeContext";
import "./styles/global.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <AuthProvider>
      <ThemeProvider>
        <App />
      </ThemeProvider>
    </AuthProvider>
  </React.StrictMode>
);
body.light { background: #fff; color: #000; }
body.dark { background: #121212; color: #fff; }
button { padding: 5px 10px; margin: 3px; cursor: pointer; }
textarea { font-family: monospace; }
body.light { background: #fff; color: #000; }
body.dark { background: #121212; color: #fff; }
button { padding: 5px 10px; margin: 3px; cursor: pointer; }
textarea { font-family: monospace; }
import { useState } from "react";
import { useAuth } from "../context/AuthContext";

export default function AuthPanel() {
  const { signup, login } = useAuth();
  const [mode, setMode] = useState("login");
  const [form, setForm] = useState({ email: "", password: "", age: 10, region: "" });

  const handleSubmit = () => {
    if (mode === "login") login(form);
    else signup(form);
  };

  return (
    <div>
      <h2>{mode === "login" ? "Login" : "Sign Up"}</h2>
      <input placeholder="Email" value={form.email} onChange={e => setForm({ ...form, email: e.target.value })} />
      <input placeholder="Password" type="password" value={form.password} onChange={e => setForm({ ...form, password: e.target.value })} />
      {mode === "signup" && <>
        <input type="number" min="10" placeholder="Age" value={form.age} onChange={e => setForm({ ...form, age: e.target.value })} />
        <input placeholder="Region" value={form.region} onChange={e => setForm({ ...form, region: e.target.value })} />
      </>}
      <button onClick={handleSubmit}>{mode === "login" ? "Login" : "Sign Up"}</button>
      <p onClick={() => setMode(mode === "login" ? "signup" : "login")} style={{ cursor: "pointer", color: "blue" }}>
        {mode === "login" ? "Create account" : "Already have account? Login"}
      </p>
    </div>
  );
}
import { useAuth } from "../context/AuthContext";
export default function DoodleCenter() {
  const { user } = useAuth();
  if (!user) return <p>Sign up to draw your own pictures!</p>;
  return (
    <div>
      <h2>Doodle Center</h2>
      <p>Draw your own picture! (Canvas goes here)</p>
      <canvas width="400" height="300" style={{ border: "1px solid #000" }}></canvas>
    </div>
  );
}
import { useAuth } from "../context/AuthContext";
import { saveToLibrary } from "../utils/storage";
export default function ImageGenerator() {
  const { user } = useAuth();
  if (!user) return <p>Sign up to generate AI pictures!</p>;

  const generate = () => {
    const url = "https://via.placeholder.com/150?text=AI+Image"; // placeholder
    saveToLibrary(url);
    alert("Image generated and saved to Library!");
  };

  return (
    <div>
      <h2>AI Image Generator</h2>
      <button onClick={generate}>Generate your own picture!</button>
    </div>
  );
}
import { useState } from "react";
export default function UltraCodePro() {
  const [code, setCode] = useState("");
  const [preview, setPreview] = useState("");

  return (
    <div>
      <h2>Ultra Code</h2>
      <textarea style={{ width: "100%", height: "150px" }} value={code} onChange={e => setCode(e.target.value)} placeholder="Write your code here..."></textarea>
      <button onClick={() => setPreview(code)}>Preview</button>
      <div style={{ marginTop: "10px", border: "1px solid #ccc", padding: "10px" }}>
        <strong>Preview:</strong>
        <div>{preview}</div>
      </div>
    </div>
  );
}
import { useAuth } from "../context/AuthContext";
export default function ShareButton() {
  const { user } = useAuth();
  if (!user) return null;
  return <button onClick={() => alert("Share options (Twitter, Facebook, etc.)")}>Share</button>;
}
import { useState, useEffect } from "react";
import { useAuth } from "../context/AuthContext";

const ACCENTS = {
  "American": ["Friendly Optimist", "Calm Professional"],
  "British": ["Witty Polite", "Measured Analyst"],
  "Indian": ["Encouraging Mentor", "Clear Problem-Solver"],
  "Chinese": ["Focused Strategist", "Helpful Guide"],
  "Russian": ["Direct Thinker", "Analytical Planner"],
  "German": ["Precise Engineer", "Structured Coach"],
  "Australian": ["Upbeat Mate", "Practical Advisor"],
  "Korean": ["Respectful Helper", "Detail-Oriented Planner"]
  // add more as needed
};

export default function Chat() {
  const { user } = useAuth();
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");
  const [accent, setAccent] = useState("American");
  const [personality, setPersonality] = useState(ACCENTS[accent][0]);

  const handleSend = () => {
    if (!input.trim()) return;
    const userMsg = { role: "user", text: input };
    setMessages(prev => [...prev, userMsg]);
    setInput("");

    // Generate 3 different responses
    const responses = [
      `(${accent} • ${personality}) Ultra says: Here's one way to answer "${input}"`,
      `(${accent} • ${personality}) Ultra thinks: Another take on "${input}"`,
      `(${accent} • ${personality}) Ultra suggests: Also consider "${input}"`
    ];

    // Randomly pick one
    const reply = responses[Math.floor(Math.random() * responses.length)];
    setMessages(prev => [...prev, { role: "assistant", text: reply }]);
  };

  useEffect(() => {
    // Update personality if accent changes
    setPersonality(ACCENTS[accent][0]);
  }, [accent]);

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%" }}>
      <div style={{ flex: 1, overflowY: "auto", padding: 10 }}>
        {messages.map((m, i) => (
          <div key={i} style={{ marginBottom: "10px", color: m.role === "assistant" ? "cyan" : "white" }}>
            <strong>{m.role === "assistant" ? "Ultra" : "You"}:</strong> {m.text}
          </div>
        ))}
      </div>
      <div style={{ display: "flex", gap: "5px" }}>
        <input
          style={{ flex: 1 }}
          placeholder="Ask Away!"
          value={input}
          onChange={e => setInput(e.target.value)}
          onKeyDown={e => e.key === "Enter" && handleSend()}
        />
        <button onClick={handleSend}>Send</button>
        <select value={accent} onChange={e => setAccent(e.target.value)}>
          {Object.keys(ACCENTS).map(a => <option key={a}>{a}</option>)}
        </select>
        <select value={personality} onChange={e => setPersonality(e.target.value)}>
          {ACCENTS[accent].map(p => <option key={p}>{p}</option>)}
        </select>
      </div>
    </div>
  );
}
import { useState, useEffect } from "react";
import { useAuth } from "../context/AuthContext";

const ACCENTS = {
  "American": ["Friendly Optimist", "Calm Professional"],
  "British": ["Witty Polite", "Measured Analyst"],
  "Indian": ["Encouraging Mentor", "Clear Problem-Solver"],
  "Chinese": ["Focused Strategist", "Helpful Guide"],
  "Russian": ["Direct Thinker", "Analytical Planner"],
  "German": ["Precise Engineer", "Structured Coach"],
  "Australian": ["Upbeat Mate", "Practical Advisor"],
  "Korean": ["Respectful Helper", "Detail-Oriented Planner"]
  // add more as needed
};

export default function Chat() {
  const { user } = useAuth();
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");
  const [accent, setAccent] = useState("American");
  const [personality, setPersonality] = useState(ACCENTS[accent][0]);

  const handleSend = () => {
    if (!input.trim()) return;
    const userMsg = { role: "user", text: input };
    setMessages(prev => [...prev, userMsg]);
    setInput("");

    // Generate 3 “thinking out loud” responses
    const responses = [
      `(${accent} • ${personality}) Ultra thinks: One way to approach "${input}"...`,
      `(${accent} • ${personality}) Ultra also suggests: Another perspective on "${input}"...`,
      `(${accent} • ${personality}) Ultra adds: You might also consider "${input}" in this way...`
    ];

    // Add all 3 responses
    const assistantMsgs = responses.map(r => ({ role: "assistant", text: r }));
    setMessages(prev => [...prev, ...assistantMsgs]);
  };

  useEffect(() => {
    // Update personality if accent changes
    setPersonality(ACCENTS[accent][0]);
  }, [accent]);

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%" }}>
      {/* Chat messages */}
      <div style={{ flex: 1, overflowY: "auto", padding: 10 }}>
        {messages.map((m, i) => (
          <div key={i} style={{ marginBottom: "10px", color: m.role === "assistant" ? "cyan" : "white" }}>
            <strong>{m.role === "assistant" ? "Ultra" : "You"}:</strong> {m.text}
          </div>
        ))}
      </div>

      {/* Input & options */}
      <div style={{ display: "flex", gap: "5px" }}>
        <input
          style={{ flex: 1 }}
          placeholder="Ask Away!"
          value={input}
          onChange={e => setInput(e.target.value)}
          onKeyDown={e => e.key === "Enter" && handleSend()}
        />
        <button onClick={handleSend}>Send</button>
        <select value={accent} onChange={e => setAccent(e.target.value)}>
          {Object.keys(ACCENTS).map(a => <option key={a}>{a}</option>)}
        </select>
        <select value={personality} onChange={e => setPersonality(e.target.value)}>
          {ACCENTS[accent].map(p => <option key={p}>{p}</option>)}
        </select>
      </div>
    </div>
  );
}
import { useState, useEffect, useRef } from "react";
import { useAuth } from "../context/AuthContext";

const ACCENTS = {
  "American": ["Friendly Optimist", "Calm Professional"],
  "British": ["Witty Polite", "Measured Analyst"],
  "Indian": ["Encouraging Mentor", "Clear Problem-Solver"],
  "Chinese": ["Focused Strategist", "Helpful Guide"],
  "Russian": ["Direct Thinker", "Analytical Planner"],
  "German": ["Precise Engineer", "Structured Coach"],
  "Australian": ["Upbeat Mate", "Practical Advisor"],
  "Korean": ["Respectful Helper", "Detail-Oriented Planner"]
};

export default function Chat() {
  const { user } = useAuth();
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");
  const [accent, setAccent] = useState("American");
  const [personality, setPersonality] = useState(ACCENTS[accent][0]);
  const synthRef = useRef(window.speechSynthesis);

  // Load chat history per user
  useEffect(() => {
    if (user) {
      const saved = JSON.parse(localStorage.getItem(`ultra_chat_${user.email}`)) || [];
      setMessages(saved);
    }
  }, [user]);

  // Save chat history per user
  useEffect(() => {
    if (user) {
      localStorage.setItem(`ultra_chat_${user.email}`, JSON.stringify(messages));
    }
  }, [messages, user]);

  const speak = (text) => {
    if (!user) return; // voice mode only for logged-in users
    const utterance = new SpeechSynthesisUtterance(text);
    utterance.lang = "en-US";
    synthRef.current.cancel();
    synthRef.current.speak(utterance);
  };

  const handleSend = () => {
    if (!input.trim()) return;
    const userMsg = { role: "user", text: input };
    setMessages(prev => [...prev, userMsg]);
    setInput("");

    const responses = [
      `(${accent} • ${personality}) Ultra thinks: One way to approach "${input}"...`,
      `(${accent} • ${personality}) Ultra also suggests: Another perspective on "${input}"...`,
      `(${accent} • ${personality}) Ultra adds: You might also consider "${input}" in this way...`
    ];

    const assistantMsgs = responses.map(r => ({ role: "assistant", text: r }));
    setMessages(prev => [...prev, ...assistantMsgs]);

    // Speak all responses
    assistantMsgs.forEach(m => speak(m.text));
  };

  useEffect(() => { setPersonality(ACCENTS[accent][0]); }, [accent]);

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%" }}>
      <div style={{ flex: 1, overflowY: "auto", padding: 10 }}>
        {messages.map((m, i) => (
          <div
            key={i}
            style={{
              marginBottom: "10px",
              color: m.role === "assistant" ? "cyan" : "white",
              background: m.role === "assistant" ? "rgba(0,255,255,0.1)" : "transparent",
              padding: m.role === "assistant" ? "5px" : "0px",
              borderRadius: "5px"
            }}
          >
            <strong>{m.role === "assistant" ? "Ultra" : "You"}:</strong> {m.text}
          </div>
        ))}
      </div>

      <div style={{ display: "flex", gap: "5px" }}>
        <input
          style={{ flex: 1 }}
          placeholder="Ask Away!"
          value={input}
          onChange={e => setInput(e.target.value)}
          onKeyDown={e => e.key === "Enter" && handleSend()}
        />
        <button onClick={handleSend}>Send</button>
        <select value={accent} onChange={e => setAccent(e.target.value)}>
          {Object.keys(ACCENTS).map(a => <option key={a}>{a}</option>)}
        </select>
        <select value={personality} onChange={e => setPersonality(e.target.value)}>
          {ACCENTS[accent].map(p => <option key={p}>{p}</option>)}
        </select>
        {user && <>
          <button onClick={() => synthRef.current.cancel()}>⏹ Stop Voice</button>
          <button onClick={() => synthRef.current.pause()}>⏸ Pause</button>
          <button onClick={() => synthRef.current.resume()}>▶ Resume</button>
        </>}
      </div>
    </div>
  );
}
import { useState, useEffect, useRef } from "react";
import { useAuth } from "../context/AuthContext";

const ACCENTS = {
  "American": ["Friendly Optimist", "Calm Professional"],
  "British": ["Witty Polite", "Measured Analyst"],
  "Indian": ["Encouraging Mentor", "Clear Problem-Solver"],
  "Chinese": ["Focused Strategist", "Helpful Guide"],
  "Russian": ["Direct Thinker", "Analytical Planner"],
  "German": ["Precise Engineer", "Structured Coach"],
  "Australian": ["Upbeat Mate", "Practical Advisor"],
  "Korean": ["Respectful Helper", "Detail-Oriented Planner"]
};

const ACCENT_LANG = {
  "American": "en-US",
  "British": "en-GB",
  "Indian": "en-IN",
  "Chinese": "zh-CN",
  "Russian": "ru-RU",
  "German": "de-DE",
  "Australian": "en-AU",
  "Korean": "ko-KR"
};

export default function Chat() {
  const { user } = useAuth();
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");
  const [accent, setAccent] = useState("American");
  const [personality, setPersonality] = useState(ACCENTS[accent][0]);
  const synthRef = useRef(window.speechSynthesis);
  const voicesRef = useRef([]);

  useEffect(() => {
    voicesRef.current = synthRef.current.getVoices();
    if (!voicesRef.current.length) {
      synthRef.current.onvoiceschanged = () => {
        voicesRef.current = synthRef.current.getVoices();
      };
    }
  }, []);

  const speak = (text) => {
    if (!user) return; // voice mode only for logged-in users
    const utterance = new SpeechSynthesisUtterance(text);
    // pick the voice matching selected accent
    const lang = ACCENT_LANG[accent] || "en-US";
    const voice = voicesRef.current.find(v => v.lang === lang) || null;
    if (voice) utterance.voice = voice;
    synthRef.current.cancel();
    synthRef.current.speak(utterance);
  };

  const handleSend = () => {
    if (!input.trim()) return;
    const userMsg = { role: "user", text: input };
    setMessages(prev => [...prev, userMsg]);
    setInput("");

    const responses = [
      `(${accent} • ${personality}) Ultra thinks: One way to approach "${input}"...`,
      `(${accent} • ${personality}) Ultra also suggests: Another perspective on "${input}"...`,
      `(${accent} • ${personality}) Ultra adds: You might also consider "${input}" in this way...`
    ];

    const assistantMsgs = responses.map(r => ({ role: "assistant", text: r }));
    setMessages(prev => [...prev, ...assistantMsgs]);

    // speak all responses with accent
    assistantMsgs.forEach(m => speak(m.text));
  };

  useEffect(() => { setPersonality(ACCENTS[accent][0]); }, [accent]);

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%" }}>
      <div style={{ flex: 1, overflowY: "auto", padding: 10 }}>
        {messages.map((m, i) => (
          <div
            key={i}
            style={{
              marginBottom: "10px",
              color: m.role === "assistant" ? "cyan" : "white",
              background: m.role === "assistant" ? "rgba(0,255,255,0.1)" : "transparent",
              padding: m.role === "assistant" ? "5px" : "0px",
              borderRadius: "5px"
            }}
          >
            <strong>{m.role === "assistant" ? "Ultra" : "You"}:</strong> {m.text}
          </div>
        ))}
      </div>

      <div style={{ display: "flex", gap: "5px" }}>
        <input
          style={{ flex: 1 }}
          placeholder="Ask Away!"
          value={input}
          onChange={e => setInput(e.target.value)}
          onKeyDown={e => e.key === "Enter" && handleSend()}
        />
        <button onClick={handleSend}>Send</button>
        <select value={accent} onChange={e => setAccent(e.target.value)}>
          {Object.keys(ACCENTS).map(a => <option key={a}>{a}</option>)}
        </select>
        <select value={personality} onChange={e => setPersonality(e.target.value)}>
          {ACCENTS[accent].map(p => <option key={p}>{p}</option>)}
        </select>
        {user && <>
          <button onClick={() => synthRef.current.cancel()}>⏹ Stop Voice</button>
          <button onClick={() => synthRef.current.pause()}>⏸ Pause</button>
          <button onClick={() => synthRef.current.resume()}>▶ Resume</button>
        </>}
      </div>
    </div>
  );
}
import { useState, useEffect, useRef } from "react";
import { useAuth } from "../context/AuthContext";

const ACCENTS = {
  "American": ["Friendly Optimist", "Calm Professional"],
  "British": ["Witty Polite", "Measured Analyst"],
  "Indian": ["Encouraging Mentor", "Clear Problem-Solver"],
  "Chinese": ["Focused Strategist", "Helpful Guide"],
  "Russian": ["Direct Thinker", "Analytical Planner"],
  "German": ["Precise Engineer", "Structured Coach"],
  "Australian": ["Upbeat Mate", "Practical Advisor"],
  "Korean": ["Respectful Helper", "Detail-Oriented Planner"]
};

const ACCENT_LANG = {
  "American": "en-US",
  "British": "en-GB",
  "Indian": "en-IN",
  "Chinese": "zh-CN",
  "Russian": "ru-RU",
  "German": "de-DE",
  "Australian": "en-AU",
  "Korean": "ko-KR"
};

// Personality templates
const PERSONALITY_STYLE = {
  "Friendly Optimist": msg => `🌟 Great news! Here's a cheerful take: ${msg}`,
  "Calm Professional": msg => `📌 Step by step: ${msg}`,
  "Witty Polite": msg => `😏 Here's a witty thought: ${msg}`,
  "Measured Analyst": msg => `🔍 Analyzing logically: ${msg}`,
  "Encouraging Mentor": msg => `💡 Keep it up! Consider: ${msg}`,
  "Clear Problem-Solver": msg => `✅ Solution: ${msg}`,
  "Focused Strategist": msg => `🎯 Strategy plan: ${msg}`,
  "Helpful Guide": msg => `🧭 Let me guide you: ${msg}`,
  "Direct Thinker": msg => `⚡ Straight answer: ${msg}`,
  "Analytical Planner": msg => `📊 Detailed plan: ${msg}`,
  "Precise Engineer": msg => `🛠 Precise steps: ${msg}`,
  "Structured Coach": msg => `🏗 Organized plan: ${msg}`,
  "Upbeat Mate": msg => `😃 Friendly advice: ${msg}`,
  "Practical Advisor": msg => `💼 Practical tip: ${msg}`,
  "Respectful Helper": msg => `🙏 Here’s my help: ${msg}`,
  "Detail-Oriented Planner": msg => `📌 Detailed guide: ${msg}`
};

export default function Chat() {
  const { user } = useAuth();
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");
  const [accent, setAccent] = useState("American");
  const [personality, setPersonality] = useState(ACCENTS[accent][0]);
  const synthRef = useRef(window.speechSynthesis);
  const voicesRef = useRef([]);

  useEffect(() => {
    voicesRef.current = synthRef.current.getVoices();
    if (!voicesRef.current.length) {
      synthRef.current.onvoiceschanged = () => {
        voicesRef.current = synthRef.current.getVoices();
      };
    }
  }, []);

  const speak = (text) => {
    if (!user) return;
    const utterance = new SpeechSynthesisUtterance(text);
    const lang = ACCENT_LANG[accent] || "en-US";
    const voice = voicesRef.current.find(v => v.lang === lang) || null;
    if (voice) utterance.voice = voice;
    synthRef.current.cancel();
    synthRef.current.speak(utterance);
  };

  const handleSend = () => {
    if (!input.trim()) return;
    const userMsg = { role: "user", text: input };
    setMessages(prev => [...prev, userMsg]);
    setInput("");

    const baseResponses = [
      `One way to approach "${input}"...`,
      `Another perspective on "${input}"...`,
      `You might also consider "${input}" in this way...`
    ];

    const assistantMsgs = baseResponses.map(r => {
      const styled = PERSONALITY_STYLE[personality] ? PERSONALITY_STYLE[personality](r) : r;
      return { role: "assistant", text: styled };
    });

    setMessages(prev => [...prev, ...assistantMsgs]);
    assistantMsgs.forEach(m => speak(m.text));
  };

  useEffect(() => { setPersonality(ACCENTS[accent][0]); }, [accent]);

  return (
    <div style={{ display: "flex", flexDirection: "column", height: "100%" }}>
      <div style={{ flex: 1, overflowY: "auto", padding: 10 }}>
        {messages.map((m, i) => (
          <div key={i} style={{
            marginBottom: "10px",
            color: m.role === "assistant" ? "cyan" : "white",
            background: m.role === "assistant" ? "rgba(0,255,255,0.1)" : "transparent",
            padding: m.role === "assistant" ? "5px" : "0px",
            borderRadius: "5px"
          }}>
            <strong>{m.role === "assistant" ? "Ultra" : "You"}:</strong> {m.text}
          </div>
        ))}
      </div>

      <div style={{ display: "flex", gap: "5px" }}>
        <input
          style={{ flex: 1 }}
          placeholder="Ask Away!"
          value={input}
          onChange={e => setInput(e.target.value)}
          onKeyDown={e => e.key === "Enter" && handleSend()}
        />
        <button onClick={handleSend}>Send</button>
        <select value={accent} onChange={e => setAccent(e.target.value)}>
          {Object.keys(ACCENTS).map(a => <option key={a}>{a}</option>)}
        </select>
        <select value={personality} onChange={e => setPersonality(e.target.value)}>
          {ACCENTS[accent].map(p => <option key={p}>{p}</option>)}
        </select>
        {user && <>
          <button onClick={() => synthRef.current.cancel()}>⏹ Stop Voice</button>
          <button onClick={() => synthRef.current.pause()}>⏸ Pause</button>
          <button onClick={() => synthRef.current.resume()}>▶ Resume</button>
        </>}
      </div>
    </div>
  );
}
import React, { useState } from "react";
import { useAuth } from "./context/AuthContext";
import Chat from "./components/Chat";

export default function App() {
  const { user } = useAuth();
  const [activeTab, setActiveTab] = useState("Chat");
  
  const tabs = ["Chat", "Ultra Code", "Library", "Doodle Center"];

  const renderTab = () => {
    switch(activeTab) {
      case "Chat": return <Chat />;
      case "Ultra Code":
        return (
          <div>
            <h2>Ultra Code</h2>
            <p>{user ? "Edit and preview your code here." : "Sign up to edit and save code."}</p>
          </div>
        );
      case "Library":
        return (
          <div>
            <h2>Library</h2>
            {user ? (
              <>
                <button style={{backgroundColor:"purple", color:"white"}}>＋ Generate your own picture!</button>
                <div>Your saved/generated images appear here.</div>
              </>
            ) : <p>Sign up to generate and save images.</p>}
          </div>
        );
      case "Doodle Center":
        return (
          <div>
            <h2>Doodle Center</h2>
            {user ? <p>Draw your own pictures here.</p> : <p>Sign up to draw and save your doodles.</p>}
          </div>
        );
      default: return null;
    }
  };

  return (
    <div style={{display:"flex", height:"100vh"}}>
      <aside style={{width:280, background:"#111", color:"white", padding:10, display:"flex", flexDirection:"column"}}>
        <div style={{display:"flex", justifyContent:"space-between"}}>
          <div style={{fontWeight:"bold", fontSize:24}}>U ★★★★★</div>
          <button onClick={()=>alert("Close Sidebar")}>X</button>
        </div>
        <div style={{marginTop:10}}>
          {tabs.map(t => (
            <button
              key={t}
              style={{display:"block", width:"100%", padding:5, marginBottom:5, background: activeTab===t ? "#333" : "#222", color:"white"}}
              onClick={()=>setActiveTab(t)}
            >{t}</button>
          ))}
        </div>
      </aside>
      <main style={{flex:1, background:"#222", color:"white", padding:20}}>
        {renderTab()}
      </main>
    </div>
  );
}
import React, { useState } from "react";
import { useAuth } from "./context/AuthContext";
import Chat from "./components/Chat";

export default function App() {
  const { user } = useAuth();
  const [activeTab, setActiveTab] = useState("Chat");
  
  const tabs = ["Chat", "Ultra Code", "Library", "Doodle Center"];

  const renderTab = () => {
    switch(activeTab) {
      case "Chat": return <Chat />;
      case "Ultra Code":
        return (
          <div>
            <h2>Ultra Code</h2>
            <p>{user ? "Edit and preview your code here." : "Sign up to edit and save code."}</p>
          </div>
        );
      case "Library":
        return (
          <div>
            <h2>Library</h2>
            {user ? (
              <>
                <button style={{backgroundColor:"purple", color:"white"}}>＋ Generate your own picture!</button>
                <div>Your saved/generated images appear here.</div>
              </>
            ) : <p>Sign up to generate and save images.</p>}
          </div>
        );
      case "Doodle Center":
        return (
          <div>
            <h2>Doodle Center</h2>
            {user ? <p>Draw your own pictures here.</p> : <p>Sign up to draw and save your doodles.</p>}
          </div>
        );
      default: return null;
    }
  };

  return (
    <div style={{display:"flex", height:"100vh"}}>
      <aside style={{width:280, background:"#111", color:"white", padding:10, display:"flex", flexDirection:"column"}}>
        <div style={{display:"flex", justifyContent:"space-between"}}>
          <div style={{fontWeight:"bold", fontSize:24}}>U ★★★★★</div>
          <button onClick={()=>alert("Close Sidebar")}>X</button>
        </div>
        <div style={{marginTop:10}}>
          {tabs.map(t => (
            <button
              key={t}
              style={{display:"block", width:"100%", padding:5, marginBottom:5, background: activeTab===t ? "#333" : "#222", color:"white"}}
              onClick={()=>setActiveTab(t)}
            >{t}</button>
          ))}
        </div>
      </aside>
      <main style={{flex:1, background:"#222", color:"white", padding:20}}>
        {renderTab()}
      </main>
    </div>
  );
}
import { useState } from "react";

function SignupForm() {
  const [isHuman, setIsHuman] = useState(false);
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  const handleSignup = () => {
    if (!isHuman) {
      alert("Please verify you are human!");
      return;
    }
    // continue signup logic here
    alert(`Account created for ${email}`);
  };

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: "8px", maxWidth: 300 }}>
      <input
        type="email"
        placeholder="Email"
        value={email}
        onChange={e => setEmail(e.target.value)}
      />
      <input
        type="password"
        placeholder="Password"
        value={password}
        onChange={e => setPassword(e.target.value)}
      />
      <label style={{ display: "flex", alignItems: "center", gap: "5px" }}>
        <input
          type="checkbox"
          checked={isHuman}
          onChange={e => setIsHuman(e.target.checked)}
        />
        I am not a robot
      </label>
      <button onClick={handleSignup}>Sign Up</button>
    </div>
  );
}

export default SignupForm;
