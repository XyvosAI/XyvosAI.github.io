import streamlit as st

# Page configuration
st.set_page_config(
    page_title="PlotWise - SAT Math Desmos AI Tutor",
    page_icon="📐",
    layout="centered"
)

# Custom Color Palette & CSS Styling
# Base Color: #F3EDDD | Text/Accent Color: #1E2421
st.markdown("""
    <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

    html, body, [class*="css"] {
        font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
    }

    /* Main background */
    .stApp {
        background-color: #F3EDDD;
        color: #1E2421;
    }

    /* Headings */
    h1, h2, h3, h4, h5, h6 {
        color: #1E2421 !important;
        font-weight: 700;
    }

    /* Text input styling */
    .stTextInput>div>div>input {
        background-color: #FFFFFF;
        color: #1E2421;
        border: 2px solid #1E2421;
        border-radius: 8px;
    }

    /* Chat message cards */
    .stChatMessage {
        background-color: #E6DFC9;
        border: 1px solid #1E2421;
        border-radius: 12px;
        color: #1E2421;
        margin-bottom: 12px;
    }

    /* Bottom chat input box */
    .stChatInputContainer textarea {
        background-color: #FFFFFF !important;
        color: #1E2421 !important;
        border: 2px solid #1E2421 !important;
        border-radius: 8px;
    }

    /* Buttons */
    .stButton>button {
        background-color: #1E2421;
        color: #F3EDDD;
        border-radius: 8px;
        border: none;
        font-weight: 600;
    }

    .stButton>button:hover {
        background-color: #2D3732;
        color: #FFFFFF;
    }
    </style>
""", unsafe_allow_html=True)

# Title & Description
st.title("📐 PlotWise: SAT Math & Desmos AI Tutor")
st.markdown("##### *Master Digital SAT Math problems by solving them dynamically inside Desmos.*")
st.caption("Paste any SAT Math question (Linear Equations, Systems, Quadratics, Functions) to get a step-by-step Desmos solution strategy.")

# Disclaimer for Trademark
st.caption("*Disclaimer: PlotWise is an independent educational tool and is not officially affiliated with or endorsed by College Board or Desmos, Inc.*")

# Initialize Chat History
if "messages" not in st.session_state:
    st.session_state.messages = [
        {
            "role": "assistant",
            "content": (
                "Hello! I am **PlotWise**, your SAT Math Desmos Coach.\n\n"
                "Paste your SAT question here or ask how to plot a function! "
                "\n\n*Example question:* 'Find the intersection of $2x + y = 7$ and $x - y = 2$ using Desmos.'"
            )
        }
    ]

# Display Chat History
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.write(message["content"])

# User Input Logic
if user_prompt := st.chat_input("Enter an SAT Math question or formula..."):
    # Store user message
    st.session_state.messages.append({"role": "user", "content": user_prompt})
    with st.chat_message("user"):
        st.write(user_prompt)

    # Generate Response
    with st.chat_message("assistant"):
        response_placeholder = st.empty()
        
        # Desmos Strategy Prompt Structure
        ai_response = f"""
### **SAT Math Strategy & Desmos Steps**

1. **Desmos Setup:**
   - Open the [Desmos Graphing Calculator](https://www.desmos.com/calculator).
   - Type Line 1: Enter your first equation directly into Desmos.
   - Type Line 2: Enter your second equation or expression.

2. **Solving Question:** 
   > *"{user_prompt}"*

3. **Step-by-Step Guidance:**
   - **Intersection Points:** Click on the point where the lines or curves cross. Desmos will display the exact coordinates $(x, y)$.
   - **Vertex & Extrema:** For quadratic functions ($ax^2 + bx + c$), click on the peak or trough to find the vertex directly without using the formula $-b / 2a$.
   - **Sliders:** If the SAT problem includes unknown constants (like $k$ or $a$), add a Slider in Desmos to test different values instantly.

4. **SAT Exam Tip:** 
   Using Desmos directly on Digital SAT Math saves up to 40% of time per algebra question compared to manual calculation!
"""
        response_placeholder.markdown(ai_response)
        st.session_state.messages.append({"role": "assistant", "content": ai_response})
