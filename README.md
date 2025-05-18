# lab10
import 'package:flutter/material.dart';

void main() => runApp(MaterialApp(home: UploadPostPage()));

class UploadPostPage extends StatefulWidget {
  @override
  _UploadPostPageState createState() => _UploadPostPageState();
}

class _UploadPostPageState extends State<UploadPostPage> {
  final TextEditingController _titleController = TextEditingController();
  final TextEditingController _descriptionController = TextEditingController();

  String? fakeImagePath; // Simulated image path

  void _selectImage() {
    // DartPad cannot select real images, so we simulate it
    setState(() {
      fakeImagePath = 'https://via.placeholder.com/150';
    });
  }

  void _uploadPost() {
    String title = _titleController.text;
    String description = _descriptionController.text;

    showDialog(
      context: context,
      builder: (_) => AlertDialog(
        title: Text('Post Uploaded'),
        content: Text('Title: $title\nDescription: $description\nImage: ${fakeImagePath ?? "None"}'),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Upload Post')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: SingleChildScrollView(
          child: Column(
            children: [
              TextField(
                controller: _titleController,
                decoration: InputDecoration(labelText: 'Title'),
              ),
              SizedBox(height: 10),
              TextField(
                controller: _descriptionController,
                decoration: InputDecoration(labelText: 'Description'),
                maxLines: 3,
              ),
              SizedBox(height: 20),
              fakeImagePath != null
                  ? Image.network(fakeImagePath!, height: 150)
                  : Text("No image selected."),
              SizedBox(height: 10),
              ElevatedButton(
                onPressed: _selectImage,
                child: Text("Select Image"),
              ),
              SizedBox(height: 10),
              ElevatedButton(
                onPressed: _uploadPost,
                child: Text("Upload"),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
