<h2>Using multer to upload file in MERN</h2>

// Make sure uploads folder exists
const uploadDir = path.join(process.cwd(), "uploads");
if (!fs.existsSync(uploadDir)) {
  fs.mkdirSync(uploadDir, { recursive: true });
}

// Multer storage config
const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, uploadDir);
  },
  filename: function (req, file, cb) {
    cb(null, Date.now() + "-" + file.originalname);
  },
});

const upload = multer({ storage });

// Create post API
router.post("/create", upload.single("image"), async (req, res) => {
  try {
    const { title, content, userId } = req.body;

    const newPost = new Post({
      title,
      content,
      userId,
      image: req.file ? req.file.path : null, // Save file path in DB
    });

    await newPost.save();
    res.status(201).json({ message: "Post created successfully", post: newPost });
  } catch (error) {
    res.status(500).json({ message: "Error creating post", error });
  }
});

<h3>Uploading  Multiple Files</h3>

// Ensure 'uploads' folder exists
const uploadDir = path.join(process.cwd(), "uploads");
if (!fs.existsSync(uploadDir)) {
  fs.mkdirSync(uploadDir, { recursive: true });
  console.log("✅ 'uploads' folder created.");
}

// Multer storage setup
const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, uploadDir);
  },
  filename: function (req, file, cb) {
    const uniqueName = Date.now() + "-" + file.originalname.replace(/\s+/g, "_");
    cb(null, uniqueName);
  },
});

// Multer instance for multiple files
const upload = multer({ storage });

// Example POST API with multiple files
app.post("/create-post", upload.array("images", 5), (req, res) => {
  try {
    const { title, description } = req.body;
    const uploadedFiles = req.files.map(file => ({
      filename: file.filename,
      path: `/uploads/${file.filename}`,
    }));

    // Store post in DB
    const newPost = {
      title,
      description,
      images: uploadedFiles,
    };

    // Example: Save to MongoDB (pseudo)
    // await PostModel.create(newPost);

    res.json({
      message: "Post created successfully!",
      post: newPost,
    });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
