import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

# Page configuration
st.set_page_config(
    page_title="XyvosAI | SAT Math Desmos Tutor",
    page_icon="📐",
    layout="centered"
)

# Custom CSS styling (Modern startup style)
st.markdown("""
    <style>
    .main {
        background-color: #0e1117;
        color: #ffffff;
    }
    .stButton>button {
        background: linear-gradient(90deg, #6366f1 0%, #a855f7 100%);
        color: white;
        border: none;
        border-radius: 8px;
        font-weight: bold;
        padding: 0.5rem 1rem;
        width: 100%;
    }
    .stButton>button:hover {
        opacity: 0.9;
    }
    .card {
        background-color: #1f2937;
        padding: 20px;
        border-radius: 12px;
        border: 1px solid #374151;
        margin-bottom: 20px;
    }
    </style>
""", unsafe_allow_html=True)

# Header section
st.title("📐 XyvosAI")
st.caption("Your Personal SAT Math & Desmos Graphing AI Tutor")

# Sidebar navigation
st.sidebar.header("Navigation")
option = st.sidebar.selectbox(
    "Select Mode:",
    ["🤖 AI Q&A (Tutor)", "📈 Graph Analysis (Desmos Solver)", "🎯 SAT Practice Test"]
)

# Mode logic
if option == "🤖 AI Q&A (Tutor)":
    st.markdown("### 💬 Master Math with XyvosAI")
    st.write("Type your SAT math questions or functions below, and XyvosAI will guide you step-by-step.")
    
    user_query = st.text_area("Example: *How can I solve linear systems efficiently?*")
    
    if st.button("Get Answer"):
        if user_query:
            st.success("XyvosAI is analyzing...")
            st.markdown(f"""
            <div class='card'>
                <h4>💡 XyvosAI Explanation:</h4>
                <p>Regarding your query (<b>{user_query}</b>), here is the step-by-step breakdown following SAT standards...</
                
