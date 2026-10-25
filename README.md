# ai-education-content-generator
An AI-powered education platform to generate study notes, summaries, MCQs, quizzes, and educational social media content.

import streamlit as st
import random

st.set_page_config(
    page_title="AI Education Content Generator",
    page_icon="📚"
)

st.title("📚 AI Education Content Generator")
st.write("Generate study notes, summaries, and quizzes.")

topic = st.text_input("Enter your study topic")
content_type = st.selectbox(
    "Choose content type",
    ["Study Notes", "Summary", "MCQ Quiz"]
)

if st.button("Generate Content"):
    if not topic.strip():
        st.warning("Please enter a topic!")
    else:
        st.subheader(f"Topic: {topic}")

        if content_type == "Study Notes":
            st.write(f"""
            ### Study Notes: {topic}

            - Definition: Learn the basic meaning of {topic}.
            - Key concepts: Understand the main principles.
            - Applications: Explore real-world uses.
            - Revision: Review important points.
            """)

        elif content_type == "Summary":
            st.write(
                f"{topic} is an important subject. "
                "Study its definition, key concepts, "
                "applications, and practical examples."
            )

        else:
            questions = [
                {
                    "q": f"What should you learn first about {topic}?",
                    "options": [
                        "Basic concepts",
                        "Unrelated topics",
                        "Nothing",
                        "Only the title"
                    ],
                    "answer": "Basic concepts"
                },
                {
                    "q": f"How can you improve your knowledge of {topic}?",
                    "options": [
                        "Avoid revision",
                        "Practice and revise",
                        "Skip examples",
                        "Never ask questions"
                    ],
                    "answer": "Practice and revise"
                }
            ]

            score = 0

            for i, question in enumerate(questions):
                st.write(f"**Q{i + 1}. {question['q']}**")
                answer = st.radio(
                    f"Select answer for question {i + 1}",
                    question["options"],
                    key=f"question_{i}"
                )

                if answer == question["answer"]:
                    score += 1

            if st.button("Check Score"):
                st.success(f"Your score: {score}/{len(questions)}")

st.caption("Educational demo project.")
