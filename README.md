 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>My Notes App</title>
  <style>
    body {
      font-family: 'Poppins', sans-serif;
      background: #f4f7fb;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }

    header {
      background-color: #4a6cf7;
      color: white;
      padding: 1rem 2rem;
      text-align: center;
      width: 100%;
      font-size: 1.5rem;
      font-weight: bold;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    }

    #noteInput {
      width: 90%;
      max-width: 600px;
      margin: 20px 0;
      padding: 12px;
      border: 2px solid #4a6cf7;
      border-radius: 10px;
      font-size: 1rem;
      outline: none;
    }

    #addNoteBtn {
      background-color: #4a6cf7;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 1rem;
      transition: 0.2s ease;
    }

    #addNoteBtn:hover {
      background-color: #3b58d2;
    }

    .notes-container {
      width: 90%;
      max-width: 600px;
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-bottom: 50px;
    }

    .note {
      background: white;
      border-radius: 10px;
      padding: 15px;
      border: 1px solid #ddd;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    }

    .note p {
      margin: 0;
      font-size: 1rem;
      color: #333;
    }

    .delete-btn {
      background: crimson;
      color: white;
      border: none;
      padding: 5px 10px;
      border-radius: 6px;
      cursor: pointer;
    }

    .delete-btn:hover {
      background: darkred;
    }
  </style>
</head>
<body>

  <header>📝 My Notes</header>

  <textarea id="noteInput" rows="4" placeholder="Write your note here..."></textarea>
  <button id="addNoteBtn">Add Note</button>

  <div class="notes-container" id="notesContainer"></div>

  <script>
    const addNoteBtn = document.getElementById('addNoteBtn');
    const noteInput = document.getElementById('noteInput');
    const notesContainer = document.getElementById('notesContainer');

    // Load saved notes
    const savedNotes = JSON.parse(localStorage.getItem('notes')) || [];
    savedNotes.forEach(note => addNote(note));

    addNoteBtn.addEventListener('click', () => {
      const noteText = noteInput.value.trim();
      if (noteText === '') return alert('Please write something!');
      addNote(noteText);
      saveNote(noteText);
      noteInput.value = '';
    });

    function addNote(text) {
      const noteDiv = document.createElement('div');
      noteDiv.classList.add('note');
      noteDiv.innerHTML = `
        <p>${text}</p>
        <button class="delete-btn">Delete</button>
      `;
      notesContainer.appendChild(noteDiv);

      noteDiv.querySelector('.delete-btn').addEventListener('click', () => {
        noteDiv.remove();
        removeNote(text);
      });
    }

    function saveNote(text) {
      const notes = JSON.parse(localStorage.getItem('notes')) || [];
      notes.push(text);
      localStorage.setItem('notes', JSON.stringify(notes));
    }

    function removeNote(text) {
      const notes = JSON.parse(localStorage.getItem('notes')) || [];
      const updatedNotes = notes.filter(note => note !== text);
      localStorage.setItem('notes', JSON.stringify(updatedNotes));
    }
  </script>

</body>
</html><img width="4148" height="2333" alt="1000035098" src="https://github.com/user-attachments/assets/81077bfa-9700-4a5a-a6fd-32f6590e4ab7" />
