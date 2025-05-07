// Reemplaza estos datos con tu configuración de Firebase
const firebaseConfig = {
  apiKey: "AIzaSyC9nKHQuB8eUvp0BDtlyx9q4QpvyfpJnOA",
  authDomain: "sorteo-destinos-vite.firebaseapp.com",
  projectId: "sorteo-destinos-vite",
  storageBucket: "sorteo-destinos-vite.firebasestorage.app",
  messagingSenderId: "26006019408",
  appId: "1:26006019408:web:8e3d1af9a700dae5686055",
};

const app = firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

document.getElementById('sorteoForm').addEventListener('submit', async (e) => {
  e.preventDefault();

  const nombre = document.getElementById('nombre').value.trim();
  const email = document.getElementById('email').value.trim();
  const telefono = document.getElementById('telefono').value.trim();

  try {
    await db.collection('registrosSorteo').add({
      nombre,
      email,
      telefono,
      timestamp: new Date()
    });

    document.getElementById('mensaje').textContent = "¡Registro exitoso!";
    document.getElementById('sorteoForm').reset();
  } catch (error) {
    document.getElementById('mensaje').textContent = "Hubo un error. Intenta de nuevo.";
    console.error(error);
  }
});
