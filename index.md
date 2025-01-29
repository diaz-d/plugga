---
title: Notes
---
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { Plus, Trash } from "lucide-react";

export default function NotesApp() {
  const [notes, setNotes] = useState([]);
  const [newTitle, setNewTitle] = useState("");
  const [newContent, setNewContent] = useState("");

  const addNote = () => {
    if (!newTitle.trim() || !newContent.trim()) return;
    setNotes([...notes, { id: Date.now(), title: newTitle, content: newContent }]);
    setNewTitle("");
    setNewContent("");
  };

  const deleteNote = (id) => {
    setNotes(notes.filter(note => note.id !== id));
  };

  return (
    <div className="max-w-2xl mx-auto p-4">
      <h1 className="text-2xl font-bold mb-4">GitHub Notes</h1>
      <div className="mb-4 space-y-2">
        <Input
          placeholder="Note Title"
          value={newTitle}
          onChange={(e) => setNewTitle(e.target.value)}
        />
        <Textarea
          placeholder="Note Content"
          value={newContent}
          onChange={(e) => setNewContent(e.target.value)}
        />
        <Button onClick={addNote} className="w-full flex items-center gap-2">
          <Plus size={16} /> Add Note
        </Button>
      </div>
      <div className="space-y-4">
        {notes.map((note) => (
          <Card key={note.id} className="p-4">
            <CardContent>
              <h2 className="text-lg font-semibold">{note.title}</h2>
              <p className="text-gray-600">{note.content}</p>
              <Button onClick={() => deleteNote(note.id)} variant="destructive" className="mt-2 flex items-center gap-2">
                <Trash size={16} /> Delete
              </Button>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}

