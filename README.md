const express = require("express");
const multer = require("multer");
const path = require("path");
const router = express.Router();

// Storage setup
const storage = multer.diskStorage({
  destination: "./uploads/",
  filename: (req, file, cb) => cb(null, Date.now() + path.extname(file.originalname))
});
const upload = multer({ storage: storage });

// POST: Upload pest image
router.post("/upload", upload.single("image"), (req, res) => {
  if (!req.file) return res.status(400).json({ message: "No file uploaded" });

  // 🔹 Placeholder AI logic: call ML model here
  res.json({
    message: "Image uploaded successfully",
    filePath: `/uploads/${req.file.filename}`,
    diagnosis: "Detected: Possible Pest (AI integration pending)"
  });
});

module.exports = router;
