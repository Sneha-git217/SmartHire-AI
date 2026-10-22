
from flask import Flask, render_template, request
import fitz
import re

app = Flask(__name__)

SKILLS = [
    "python", "java", "javascript", "typescript", "html", "css", "react",
    "node.js", "node", "flask", "django", "fastapi", "sql", "mysql",
    "mongodb", "postgresql", "git", "github", "docker", "aws", "azure",
    "machine learning", "deep learning", "artificial intelligence", "ai",
    "data analysis", "pandas", "numpy", "scikit-learn", "tensorflow",
    "power bi", "excel", "rest api", "api"
]

def extract_pdf_text(file):
    doc = fitz.open(stream=file.read(), filetype="pdf")
    return "\n".join(page.get_text() for page in doc)

def find_skills(text):
    t = text.lower()
    found = []
    for skill in SKILLS:
        if skill in t:
            found.append(skill.title() if skill != "ai" else "AI")
    return sorted(set(found))

def keywords(text):
    words = re.findall(r"[a-zA-Z][a-zA-Z+#.-]{2,}", text.lower())
    stop = {
        "the","and","for","with","you","are","our","this","that","from","have",
        "will","your","job","role","work","years","using","into","about","who",
        "they","their","they","required","experience","looking","candidate",
        "should","must","can","has","been","also","not","but","all"
    }
    counts = {}
    for w in words:
        if w not in stop:
            counts[w] = counts.get(w, 0) + 1
    return [w for w, _ in sorted(counts.items(), key=lambda x: (-x[1], x[0]))[:12]]

def analyze(resume_text, job_text):
    resume_skills = set(s.lower() for s in find_skills(resume_text))
    job_skills = set(s.lower() for s in find_skills(job_text))

    matched = sorted(resume_skills & job_skills)
    missing = sorted(job_skills - resume_skills)

    if job_skills:
        skill_score = round(len(matched) / len(job_skills) * 100)
    else:
        skill_score = 70

    job_words = set(keywords(job_text))
    resume_words = set(keywords(resume_text))
    keyword_score = round(len(job_words & resume_words) / max(len(job_words), 1) * 100)

    # A simple transparent compatibility model for the academic project.
    overall = round(skill_score * 0.70 + keyword_score * 0.30)

    recommendations = []
    if missing:
        recommendations.append("Consider learning or highlighting: " + ", ".join(missing[:5]) + ".")
    if len(resume_text.split()) < 180:
        recommendations.append("Add more detail to your projects and achievements, preferably with measurable results.")
    if "github" not in resume_text.lower():
        recommendations.append("Consider adding a GitHub/portfolio link if you have relevant projects.")
    recommendations.append("Tailor the resume wording to the most important requirements in the job description.")

    questions = []
    for skill in matched[:5]:
        questions.append(f"Explain your practical experience with {skill.title()}.")
    questions += [
        "Tell us about your strongest project and your contribution to it.",
        "What technical challenge did you face and how did you solve it?",
        "Why are you interested in this role?"
    ]

    return {
        "overall": overall,
        "skill_score": skill_score,
        "keyword_score": keyword_score,
        "matched": [x.title() for x in matched],
        "missing": [x.title() for x in missing],
        "recommendations": recommendations,
        "questions": questions[:7]
    }

@app.route("/", methods=["GET", "POST"])
def index():
    result = None
    error = None
    resume_preview = ""
    if request.method == "POST":
        resume = request.files.get("resume")
        job = request.form.get("job_description", "").strip()
        if not resume or not resume.filename.lower().endswith(".pdf"):
            error = "Please upload a PDF resume."
        elif not job:
            error = "Please paste a job description."
        else:
            try:
                resume_text = extract_pdf_text(resume)
                if not resume_text.strip():
                    error = "Could not extract text from the PDF. Try a text-based PDF."
                else:
                    result = analyze(resume_text, job)
                    resume_preview = resume_text[:500]
            except Exception as exc:
                error = f"Could not read the PDF: {exc}"
    return render_template("index.html", result=result, error=error, resume_preview=resume_preview)

if __name__ == "__main__":
    app.run(debug=True)
