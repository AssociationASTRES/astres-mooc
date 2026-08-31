import React, { useState, useEffect } from 'react';
import { ChevronDown, Play, CheckCircle, Award, LogOut, Menu, X } from 'lucide-react';

const COURSES = [
  {
    id: 1,
    title: "Les Fondamentaux de l'Astronomie",
    description: "Découvrez les bases de l'univers",
    duration: "45 min",
    lessons: [
      { id: 1, title: "Introduction au Cosmos", type: "video", videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ", duration: 8 },
      { id: 2, title: "Les Constellations", type: "text", content: "Les constellations sont des groupes d'étoiles formant des motifs dans le ciel nocturne. Il existe 88 constellations officielles reconnues internationalement.", duration: 5 },
      { id: 3, title: "Quiz: Les Bases", type: "quiz", questions: [
        { id: 1, question: "Combien de constellations officielles existe-t-il?", options: ["48", "88", "128", "200"], correct: 1 },
        { id: 2, question: "Quelle est l'étoile la plus proche de la Terre?", options: ["Sirius", "Proxima du Centaure", "Arcturus", "Véga"], correct: 1 },
      ], duration: 8 }
    ]
  },
  {
    id: 2,
    title: "L'Exploration Spatiale",
    description: "Un voyage à travers les missions spatiales",
    duration: "60 min",
    lessons: [
      { id: 1, title: "Histoire des Fusées", type: "video", videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ", duration: 12 },
      { id: 2, title: "Missions Célèbres", type: "text", content: "Apollo 11, Voyager, Hubble... Découvrez les missions qui ont changé notre compréhension de l'univers.", duration: 6 },
      { id: 3, title: "Quiz: Exploration Spatiale", type: "quiz", questions: [
        { id: 1, question: "En quelle année Apollo 11 a-t-elle aluni?", options: ["1967", "1969", "1971", "1973"], correct: 1 },
        { id: 2, question: "Quel télescope a révolutionné l'observation?", options: ["Galileo", "Hubble", "Kepler", "Newton"], correct: 1 },
      ], duration: 10 }
    ]
  }
];

export default function ASTRESMooc() {
  const [user, setUser] = useState(null);
  const [currentPage, setCurrentPage] = useState('login');
  const [currentCourseId, setCurrentCourseId] = useState(null);
  const [currentLessonId, setCurrentLessonId] = useState(null);
  const [progress, setProgress] = useState({});
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);

  useEffect(() => {
    const stored = localStorage.getItem('astres_user');
    const storedProgress = localStorage.getItem('astres_progress');
    if (stored) setUser(JSON.parse(stored));
    if (storedProgress) setProgress(JSON.parse(storedProgress));
  }, []);

  const handleLogin = (e, isSignup = false) => {
    e.preventDefault();
    const formData = new FormData(e.target);
    const userData = {
      name: formData.get('name'),
      email: formData.get('email'),
      id: Math.random().toString(36).substr(2, 9)
    };
    setUser(userData);
    localStorage.setItem('astres_user', JSON.stringify(userData));
    setCurrentPage('dashboard');
  };

  const handleLogout = () => {
    setUser(null);
    localStorage.removeItem('astres_user');
    setCurrentPage('login');
  };

  const handleCompleteLesson = (courseId, lessonId) => {
    const key = `${courseId}-${lessonId}`;
    const newProgress = { ...progress, [key]: true };
    setProgress(newProgress);
    localStorage.setItem('astres_progress', JSON.stringify(newProgress));
  };

  const getCourseProgress = (courseId) => {
    const course = COURSES.find(c => c.id === courseId);
    if (!course) return 0;
    const completed = course.lessons.filter(l => progress[`${courseId}-${l.id}`]).length;
    return Math.round((completed / course.lessons.length) * 100);
  };

  const getCurrentCourse = () => COURSES.find(c => c.id === currentCourseId);
  const getCurrentLesson = () => getCurrentCourse()?.lessons.find(l => l.id === currentLessonId);

  if (!user) {
    return (
      <div style={{ background: 'linear-gradient(135deg, #00d9d9 0%, #7209b7 50%, #06ffa5 100%)', minHeight: '100vh', display: 'flex', alignItems: 'center', justifyContent: 'center', padding: '20px' }}>
        <div style={{ background: 'white', borderRadius: '16px', padding: '40px', maxWidth: '400px', width: '100%', boxShadow: '0 20px 60px rgba(0,0,0,0.3)' }}>
          <h1 style={{ fontSize: '32px', color: '#000', marginBottom: '10px', textAlign: 'center', fontWeight: 'bold' }}>ASTRES</h1>
          <p style={{ fontSize: '14px', color: '#666', textAlign: 'center', marginBottom: '30px' }}>Explorez l'univers à travers nos cours</p>
          
          <form onSubmit={(e) => handleLogin(e, false)} style={{ display: 'flex', flexDirection: 'column', gap: '15px' }}>
            <input
              name="name"
              placeholder="Votre nom"
              required
              style={{ padding: '12px', border: '1px solid #ddd', borderRadius: '8px', fontSize: '14px' }}
            />
            <input
              name="email"
              type="email"
              placeholder="Votre email"
              required
              style={{ padding: '12px', border: '1px solid #ddd', borderRadius: '8px', fontSize: '14px' }}
            />
            <button
              type="submit"
              style={{
                padding: '12px',
                background: 'linear-gradient(135deg, #00d9d9 0%, #7209b7 100%)',
                color: 'white',
                border: 'none',
                borderRadius: '8px',
                fontSize: '16px',
                fontWeight: 'bold',
                cursor: 'pointer'
              }}
            >
              Commencer
            </button>
          </form>
        </div>
      </div>
    );
  }

  if (currentPage === 'lesson') {
    const lesson = getCurrentLesson();
    const course = getCurrentCourse();
    const isCompleted = progress[`${currentCourseId}-${lesson?.id}`];

    return (
      <div style={{ minHeight: '100vh', background: '#f5f5f5' }}>
        {/* Header */}
        <div style={{ background: 'linear-gradient(135deg, #00d9d9 0%, #7209b7 100%)', padding: '20px', color: 'white', display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
          <div>
            <h2 style={{ margin: '0', fontSize: '24px', fontWeight: 'bold' }}>{course?.title}</h2>
            <p style={{ margin: '5px 0 0 0', fontSize: '14px', opacity: 0.9 }}>{lesson?.title}</p>
          </div>
          <button
            onClick={() => setCurrentPage('dashboard')}
            style={{ background: 'rgba(255,255,255,0.2)', border: 'none', color: 'white', padding: '8px 16px', borderRadius: '6px', cursor: 'pointer', fontSize: '14px' }}
          >
            Retour
          </button>
        </div>

        {/* Contenu */}
        <div style={{ maxWidth: '800px', margin: '0 auto', padding: '30px 20px' }}>
          {lesson?.type === 'video' && (
            <div style={{ marginBottom: '30px', background: 'white', borderRadius: '12px', padding: '20px', boxShadow: '0 2px 8px rgba(0,0,0,0.1)' }}>
              <iframe
                width="100%"
                height="400"
                src={lesson.videoUrl}
                frameBorder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowFullScreen
                style={{ borderRadius: '8px' }}
              ></iframe>
            </div>
          )}

          {lesson?.type === 'text' && (
            <div style={{ background: 'white', borderRadius: '12px', padding: '30px', marginBottom: '30px', boxShadow: '0 2px 8px rgba(0,0,0,0.1)' }}>
              <p style={{ fontSize: '16px', lineHeight: '1.8', color: '#333' }}>{lesson.content}</p>
            </div>
          )}

          {lesson?.type === 'quiz' && (
            <Quiz questions={lesson.questions} courseId={currentCourseId} lessonId={lesson.id} onComplete={() => handleCompleteLesson(currentCourseId, lesson.id)} />
          )}

          {lesson?.type !== 'quiz' && (
            <div style={{ textAlign: 'center', marginTop: '30px' }}>
              <button
                onClick={() => handleCompleteLesson(currentCourseId, lesson?.id)}
                style={{
                  padding: '12px 30px',
                  background: isCompleted ? '#06ffa5' : 'linear-gradient(135deg, #00d9d9 0%, #7209b7 100%)',
                  color: isCompleted ? '#000' : 'white',
                  border: 'none',
                  borderRadius: '8px',
                  fontSize: '16px',
                  fontWeight: 'bold',
                  cursor: 'pointer',
                  display: 'flex',
                  alignItems: 'center',
                  gap: '8px',
                  margin: '0 auto'
                }}
              >
                {isCompleted ? <CheckCircle size={20} /> : <Play size={20} />}
                {isCompleted ? 'Leçon complétée' : 'Marquer comme complété'}
              </button>
            </div>
          )}
        </div>
      </div>
    );
  }

  return (
    <div style={{ minHeight: '100vh', background: '#f5f5f5' }}>
      {/* Header */}
      <div style={{ background: 'linear-gradient(135deg, #00d9d9 0%, #7209b7 100%)', padding: '20px', color: 'white', display: 'flex', justifyContent: 'space-between', alignItems: 'center' }}>
        <h1 style={{ margin: '0', fontSize: '28px', fontWeight: 'bold' }}>ASTRES</h1>
        <div style={{ display: 'flex', gap: '15px', alignItems: 'center' }}>
          <span style={{ fontSize: '14px' }}>Bienvenue, {user.name}</span>
          <button
            onClick={handleLogout}
            style={{ background: 'rgba(255,255,255,0.2)', border: 'none', color: 'white', padding: '8px 16px', borderRadius: '6px', cursor: 'pointer', display: 'flex', alignItems: 'center', gap: '6px' }}
          >
            <LogOut size={16} /> Déconnexion
          </button>
        </div>
      </div>

      {/* Contenu */}
      <div style={{ maxWidth: '1200px', margin: '0 auto', padding: '40px 20px' }}>
        <h2 style={{ fontSize: '28px', marginBottom: '30px', color: '#000' }}>Mes Cours</h2>
        
        <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fit, minmax(300px, 1fr))', gap: '20px' }}>
          {COURSES.map(course => {
            const courseProgress = getCourseProgress(course.id);
            return (
              <div
                key={course.id}
                style={{
                  background: 'white',
                  borderRadius: '12px',
                  overflow: 'hidden',
                  boxShadow: '0 2px 8px rgba(0,0,0,0.1)',
                  cursor: 'pointer',
                  transition: 'transform 0.2s',
                  transform: 'translateY(0)'
                }}
                onMouseEnter={(e) => e.currentTarget.style.transform = 'translateY(-4px)'}
                onMouseLeave={(e) => e.currentTarget.style.transform = 'translateY(0)'}
              >
                <div style={{ background: 'linear-gradient(135deg, #00d9d9 0%, #7209b7 100%)', height: '150px' }}></div>
                <div style={{ padding: '20px' }}>
                  <h3 style={{ fontSize: '18px', margin: '0 0 10px 0', color: '#000', fontWeight: 'bold' }}>{course.title}</h3>
                  <p style={{ fontSize: '14px', color: '#666', margin: '0 0 15px 0' }}>{course.description}</p>
                  
                  {/* Progress bar */}
                  <div style={{ marginBottom: '15px' }}>
                    <div style={{ display: 'flex', justifyContent: 'space-between', fontSize: '12px', marginBottom: '5px', color: '#666' }}>
                      <span>Progression</span>
                      <span>{courseProgress}%</span>
                    </div>
                    <div style={{ background: '#e0e0e0', height: '6px', borderRadius: '3px', overflow: 'hidden' }}>
                      <div style={{ background: 'linear-gradient(90deg, #00d9d9 0%, #06ffa5 100%)', height: '100%', width: `${courseProgress}%`, transition: 'width 0.3s' }}></div>
                    </div>
                  </div>

                  <button
                    onClick={() => {
                      setCurrentCourseId(course.id);
                      setCurrentLessonId(course.lessons[0].id);
                      setCurrentPage('lesson');
                    }}
                    style={{
                      width: '100%',
                      padding: '10px',
                      background: 'linear-gradient(135deg, #00d9d9 0%, #7209b7 100%)',
                      color: 'white',
                      border: 'none',
                      borderRadius: '6px',
                      cursor: 'pointer',
                      fontSize: '14px',
                      fontWeight: 'bold'
                    }}
                  >
                    {courseProgress === 100 ? '✓ Complété' : 'Continuer'}
                  </button>
                </div>
              </div>
            );
          })}
        </div>

        {/* Certificats */}
        <div style={{ marginTop: '50px' }}>
          <h3 style={{ fontSize: '22px', marginBottom: '20px', color: '#000' }}>Mes Certificats</h3>
          <div style={{ display: 'grid', gridTemplateColumns: 'repeat(auto-fit, minmax(250px, 1fr))', gap: '20px' }}>
            {COURSES.map(course => {
              const progress = getCourseProgress(course.id);
              return progress === 100 ? (
                <div key={course.id} style={{ background: 'white', borderRadius: '12px', padding: '20px', boxShadow: '0 2px 8px rgba(0,0,0,0.1)', textAlign: 'center' }}>
                  <Award size={40} color="#06ffa5" style={{ margin: '0 auto', marginBottom: '10px' }} />
                  <h4 style={{ fontSize: '16px', margin: '10px 0', color: '#000', fontWeight: 'bold' }}>{course.title}</h4>
                  <p style={{ fontSize: '12px', color: '#666', marginBottom: '15px' }}>Certificat d'achèvement</p>
                  <button
                    onClick={() => downloadCertificate(course.title, user.name)}
                    style={{
                      width: '100%',
                      padding: '10px',
                      background: '#06ffa5',
                      color: '#000',
                      border: 'none',
                      borderRadius: '6px',
                      cursor: 'pointer',
                      fontSize: '14px',
                      fontWeight: 'bold'
                    }}
                  >
                    Télécharger
                  </button>
                </div>
              ) : null;
            })}
          </div>
        </div>
      </div>
    </div>
  );
}

function Quiz({ questions, courseId, lessonId, onComplete }) {
  const [currentQuestion, setCurrentQuestion] = useState(0);
  const [answers, setAnswers] = useState({});
  const [showResults, setShowResults] = useState(false);

  const handleAnswer = (answerId) => {
    setAnswers({ ...answers, [currentQuestion]: answerId });
  };

  const handleSubmit = () => {
    if (Object.keys(answers).length === questions.length) {
      setShowResults(true);
    }
  };

  const getScore = () => {
    let correct = 0;
    questions.forEach((q, idx) => {
      if (answers[idx] === q.correct) correct++;
    });
    return Math.round((correct / questions.length) * 100);
  };

  if (showResults) {
    const score = getScore();
    const passed = score >= 70;
    return (
      <div style={{ background: 'white', borderRadius: '12px', padding: '30px', textAlign: 'center', boxShadow: '0 2px 8px rgba(0,0,0,0.1)' }}>
        <div style={{ fontSize: '48px', marginBottom: '20px' }}>{passed ? '🎉' : '📚'}</div>
        <h3 style={{ fontSize: '24px', marginBottom: '10px', color: '#000', fontWeight: 'bold' }}>Score: {score}%</h3>
        <p style={{ fontSize: '16px', color: '#666', marginBottom: '20px' }}>{passed ? 'Excellent! Vous avez réussi.' : 'Essayez à nouveau.'}</p>
        {passed && (
          <button
            onClick={onComplete}
            style={{
              padding: '12px 30px',
              background: '#06ffa5',
              color: '#000',
              border: 'none',
              borderRadius: '8px',
              cursor: 'pointer',
              fontSize: '16px',
              fontWeight: 'bold'
            }}
          >
            Continuer
          </button>
        )}
      </div>
    );
  }

  const q = questions[currentQuestion];
  return (
    <div style={{ background: 'white', borderRadius: '12px', padding: '30px', boxShadow: '0 2px 8px rgba(0,0,0,0.1)' }}>
      <div style={{ marginBottom: '20px' }}>
        <p style={{ fontSize: '12px', color: '#666', margin: '0' }}>Question {currentQuestion + 1} sur {questions.length}</p>
        <div style={{ background: '#e0e0e0', height: '4px', borderRadius: '2px', marginTop: '8px', overflow: 'hidden' }}>
          <div style={{ background: '#00d9d9', height: '100%', width: `${((currentQuestion + 1) / questions.length) * 100}%` }}></div>
        </div>
      </div>

      <h3 style={{ fontSize: '18px', marginBottom: '20px', color: '#000' }}>{q.question}</h3>

      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px', marginBottom: '20px' }}>
        {q.options.map((option, idx) => (
          <button
            key={idx}
            onClick={() => handleAnswer(idx)}
            style={{
              padding: '12px',
              background: answers[currentQuestion] === idx ? 'linear-gradient(135deg, #00d9d9 0%, #7209b7 100%)' : '#f0f0f0',
              color: answers[currentQuestion] === idx ? 'white' : '#000',
              border: '1px solid #ddd',
              borderRadius: '8px',
              cursor: 'pointer',
              textAlign: 'left',
              transition: 'all 0.2s'
            }}
          >
            {option}
          </button>
        ))}
      </div>

      <div style={{ display: 'flex', gap: '10px' }}>
        <button
          onClick={() => setCurrentQuestion(Math.max(0, currentQuestion - 1))}
          disabled={currentQuestion === 0}
          style={{
            flex: 1,
            padding: '12px',
            background: currentQuestion === 0 ? '#ddd' : 'white',
            border: '1px solid #ddd',
            borderRadius: '8px',
            cursor: currentQuestion === 0 ? 'default' : 'pointer'
          }}
        >
          Précédent
        </button>
        {currentQuestion < questions.length - 1 ? (
          <button
            onClick={() => setCurrentQuestion(currentQuestion + 1)}
            style={{
              flex: 1,
              padding: '12px',
              background: 'linear-gradient(135deg, #00d9d9 0%, #7209b7 100%)',
              color: 'white',
              border: 'none',
              borderRadius: '8px',
              cursor: 'pointer'
            }}
          >
            Suivant
          </button>
        ) : (
          <button
            onClick={handleSubmit}
            disabled={Object.keys(answers).length !== questions.length}
            style={{
              flex: 1,
              padding: '12px',
              background: Object.keys(answers).length === questions.length ? '#06ffa5' : '#ddd',
              color: '#000',
              border: 'none',
              borderRadius: '8px',
              cursor: Object.keys(answers).length === questions.length ? 'pointer' : 'default',
              fontWeight: 'bold'
            }}
          >
            Terminer le quiz
          </button>
        )}
      </div>
    </div>
  );
}

function downloadCertificate(courseName, userName) {
  const html = `
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="UTF-8">
      <title>Certificat</title>
      <style>
        body { margin: 0; padding: 40px; font-family: Georgia, serif; text-align: center; background: linear-gradient(135deg, #00d9d9 0%, #7209b7 100%); }
        .certificate { background: white; max-width: 800px; margin: 0 auto; padding: 60px; border-radius: 10px; box-shadow: 0 10px 40px rgba(0,0,0,0.3); }
        h1 { color: #7209b7; font-size: 48px; margin: 0; }
        .subtitle { color: #00d9d9; font-size: 18px; margin: 20px 0; }
        .content { margin: 40px 0; font-size: 18px; color: #333; }
        .name { font-size: 32px; font-weight: bold; color: #06ffa5; margin: 20px 0; }
        .course { font-size: 24px; color: #7209b7; margin: 30px 0; font-style: italic; }
        .footer { margin-top: 40px; border-top: 2px solid #00d9d9; padding-top: 20px; color: #666; font-size: 14px; }
      </style>
    </head>
    <body>
      <div class="certificate">
        <h1>ASTRES</h1>
        <div class="subtitle">Certificat d'Achèvement</div>
        <div class="content">
          <p>Ce certificat est décerné à</p>
          <div class="name">${userName}</div>
          <p>Pour avoir complété avec succès le cours</p>
          <div class="course">${courseName}</div>
          <p style="margin-top: 40px;">Délivré le ${new Date().toLocaleDateString('fr-FR')}</p>
        </div>
        <div class="footer">
          <p>ASTRES - Plateforme d'Apprentissage Spatiale</p>
        </div>
      </div>
    </body>
    </html>
  `;
  
  const element = document.createElement('a');
  element.href = 'data:text/html;charset=utf-8,' + encodeURIComponent(html);
  element.download = `certificat_${courseName}.html`;
  document.body.appendChild(element);
  element.click();
  document.body.removeChild(element);
}
