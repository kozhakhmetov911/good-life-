import { useState } from "react";

export default function App() {
  const [symptoms, setSymptoms] = useState("");
  const [result, setResult] = useState(null);

  const analyzeSymptoms = () => {
    let response = {
      causes: [],
      doctor: "",
      advice: [],
      emergency: false,
    };

    const s = symptoms.toLowerCase();

    if (s.includes("кашель") && s.includes("температура")) {
      response.causes = ["ОРВИ", "Грипп", "Бронхит"];
      response.doctor = "Терапевт";
      response.advice = [
        "Отдых",
        "Обильное питьё",
        "Жаропонижающее (парацетамол, ибупрофен)",
      ];
    } else if (s.includes("боль в груди")) {
      response.causes = ["Проблемы с сердцем", "Пневмония"];
      response.doctor = "Кардиолог / Терапевт";
      response.advice = ["Срочно обратиться в больницу"];
      response.emergency = true;
    } else if (s.includes("головная боль")) {
      response.causes = ["Мигрень", "Переутомление", "Простуда"];
      response.doctor = "Невролог / Терапевт";
      response.advice = ["Сон", "Обезболивающее", "Спокойствие"];
    } else {
      response.causes = ["Недостаточно данных"];
      response.doctor = "Обратитесь к терапевту";
      response.advice = ["Наблюдайте за состоянием"];
    }

    setResult(response);
  };

  return (
    <div style={{ minHeight: "100vh", display: "flex", justifyContent: "center", alignItems: "center", background: "#f3f4f6" }}>
      <div style={{ width: "100%", maxWidth: "600px", background: "#fff", padding: "20px", borderRadius: "16px", boxShadow: "0 4px 10px rgba(0,0,0,0.1)" }}>
        <h1 style={{ fontSize: "24px", fontWeight: "bold", textAlign: "center" }}>🩺 ИИ-онлайн ассистент здоровья</h1>
        <p style={{ fontSize: "14px", color: "#555", textAlign: "center", marginBottom: "20px" }}>
          Опишите ваши симптомы, и получите возможные причины и рекомендации.
        </p>

        <input
          type="text"
          placeholder="Например: кашель, температура 38, слабость"
          value={symptoms}
          onChange={(e) => setSymptoms(e.target.value)}
          style={{ width: "100%", padding: "10px", borderRadius: "8px", border: "1px solid #ccc", marginBottom: "10px" }}
        />
        <button
          onClick={analyzeSymptoms}
          style={{ width: "100%", padding: "10px", background: "#2563eb", color: "white", fontWeight: "bold", border: "none", borderRadius: "8px" }}
        >
          Проанализировать
        </button>

        {result && (
          <div style={{ marginTop: "20px", padding: "15px", background: "#f9fafb", borderRadius: "10px" }}>
            <h2 style={{ fontWeight: "600", marginBottom: "10px" }}>Результаты анализа:</h2>
            <p><strong>Возможные причины:</strong> {result.causes.join(", ")}</p>
            <p><strong>Рекомендуемый врач:</strong> {result.doctor}</p>
            <p><strong>Советы:</strong> {result.advice.join(", ")}</p>
            {result.emergency && (
              <p style={{ color: "red", fontWeight: "bold", marginTop: "10px" }}>
                ⚠️ Срочно обратитесь к врачу или вызовите скорую помощь!
              </p>
            )}
            <p style={{ fontSize: "12px", color: "#777", marginTop: "10px" }}>
              ⚠️ Это не медицинский диагноз. Обязательно проконсультируйтесь с врачом.
            </p>
          </div>
        )}
      </div>
    </div>
  );
}
