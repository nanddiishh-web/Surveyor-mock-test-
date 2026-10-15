I will now generate an interactive, self-contained mock test web application in English based on the KEA Land Surveyor (SSLR) Paper-II (Specific Paper) document.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>KEA Land Surveyor (SSLR) Paper-II Mock Test</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- MathJax for rendering formulas -->
  <script>
    window.MathJax = {
      tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] },
      svg: { fontCache: 'global' }
    };
  </script>
  <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
  <style>
    .glass-panel {
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(8px);
    }
  </style>
</head>
<body class="bg-slate-100 text-slate-800 font-sans antialiased min-h-screen flex flex-col">

  <!-- Header -->
  <header class="bg-indigo-900 text-white shadow-md sticky top-0 z-30">
    <div class="max-w-7xl mx-auto px-4 py-3 flex flex-wrap justify-between items-center gap-3">
      <div>
        <h1 class="text-lg md:text-xl font-bold tracking-tight">KEA Land Surveyor (SSLR) Paper-II</h1>
        <p class="text-xs text-indigo-200">Specific Paper • Duration: 120 Minutes • Total Questions: 100 • Negative Marking: 0.25</p>
      </div>
      
      <!-- Timer & Actions -->
      <div class="flex items-center gap-4">
        <div class="bg-indigo-800 border border-indigo-700 px-3 py-1.5 rounded-lg flex items-center gap-2">
          <span class="text-xs uppercase text-indigo-300 font-semibold">Time Remaining</span>
          <span id="timerDisplay" class="font-mono text-lg font-bold text-amber-300">02:00:00</span>
        </div>
        <button id="submitBtn" onclick="confirmSubmitTest()" class="bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-semibold px-4 py-2 rounded-lg transition shadow">
          Submit Exam
        </button>
      </div>
    </div>
  </header>

  <!-- Main Container -->
  <div class="max-w-7xl mx-auto px-4 py-6 flex-1 flex flex-col lg:flex-row gap-6 w-full">
    
    <!-- Question Area -->
    <main class="flex-1 glass-panel p-6 rounded-xl shadow border border-slate-200 flex flex-col justify-between">
      <div id="questionContainer">
        <!-- Question Header -->
        <div class="flex justify-between items-center pb-4 border-b border-slate-200 mb-5">
          <span class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold bg-indigo-100 text-indigo-800">
            Question <span id="currentQNum" class="ml-1">1</span> of <span id="totalQNum">100</span>
          </span>
          <span class="text-xs font-medium text-slate-500">Marks: +1.00 | -0.25</span>
        </div>

        <!-- Question Text & Figures -->
        <div id="questionText" class="text-base md:text-lg font-medium text-slate-900 leading-relaxed mb-6">
          <!-- Injected dynamically -->
        </div>

        <!-- Options Container -->
        <div id="optionsList" class="space-y-3 mb-6">
          <!-- Injected dynamically -->
        </div>
      </div>

      <!-- Navigation & Action Buttons -->
      <div class="pt-4 border-t border-slate-200 flex flex-wrap justify-between items-center gap-3">
        <div class="flex gap-2">
          <button id="prevBtn" onclick="prevQuestion()" class="px-4 py-2 text-sm font-semibold bg-slate-200 hover:bg-slate-300 text-slate-700 rounded-lg transition">
            Previous
          </button>
          <button id="nextBtn" onclick="nextQuestion()" class="px-5 py-2 text-sm font-semibold bg-indigo-600 hover:bg-indigo-700 text-white rounded-lg transition">
            Next
          </button>
        </div>
        <div class="flex gap-2">
          <button onclick="clearCurrentResponse()" class="px-3 py-2 text-xs font-medium text-slate-600 hover:text-slate-800 border border-slate-300 hover:bg-slate-100 rounded-lg transition">
            Clear Response
          </button>
          <button onclick="toggleReviewFlag()" id="reviewBtn" class="px-3 py-2 text-xs font-semibold text-amber-700 border border-amber-300 bg-amber-50 hover:bg-amber-100 rounded-lg transition">
            Mark for Review
          </button>
        </div>
      </div>
    </main>

    <!-- Sidebar: Question Palette & Summary -->
    <aside class="w-full lg:w-80 glass-panel p-5 rounded-xl shadow border border-slate-200 flex flex-col gap-5">
      <div>
        <h2 class="text-sm font-bold text-slate-800 mb-3 uppercase tracking-wider">Exam Status</h2>
        <div class="grid grid-cols-2 gap-2 text-xs font-medium">
          <div class="flex items-center gap-2"><span class="w-3.5 h-3.5 rounded bg-emerald-500 inline-block"></span> Attempted (<span id="countAnswered">0</span>)</div>
          <div class="flex items-center gap-2"><span class="w-3.5 h-3.5 rounded bg-slate-200 border border-slate-300 inline-block"></span> Unanswered (<span id="countUnanswered">100</span>)</div>
          <div class="flex items-center gap-2"><span class="w-3.5 h-3.5 rounded bg-amber-400 inline-block"></span> Marked Review (<span id="countMarked">0</span>)</div>
          <div class="flex items-center gap-2"><span class="w-3.5 h-3.5 rounded bg-indigo-600 inline-block"></span> Current</div>
        </div>
      </div>

      <!-- Question Grid -->
      <div class="flex-1">
        <h3 class="text-xs font-bold text-slate-500 uppercase tracking-wider mb-2">Question Palette</h3>
        <div id="paletteGrid" class="grid grid-cols-5 sm:grid-cols-10 lg:grid-cols-5 gap-2 max-h-96 overflow-y-auto p-1">
          <!-- Injected dynamically -->
        </div>
      </div>

      <div class="pt-3 border-t border-slate-200 text-xs text-slate-500">
        Tip: You can jump straight to any question by clicking its number in the palette above.
      </div>
    </aside>
  </div>

  <!-- Result Modal -->
  <div id="resultModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
    <div class="bg-white rounded-2xl shadow-2xl max-w-2xl w-full p-6 max-h-[90vh] overflow-y-auto">
      <div class="text-center pb-4 border-b border-slate-200">
        <h2 class="text-2xl font-bold text-slate-800">Test Evaluation Report</h2>
        <p class="text-sm text-slate-500">KEA Land Surveyor (SSLR) Paper-II</p>
      </div>

      <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 my-6 text-center">
        <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
          <div class="text-xs text-slate-500 font-semibold uppercase">Total Score</div>
          <div id="resScore" class="text-2xl font-black text-indigo-600 mt-1">0.00</div>
        </div>
        <div class="bg-emerald-50 p-3 rounded-xl border border-emerald-200">
          <div class="text-xs text-emerald-700 font-semibold uppercase">Correct</div>
          <div id="resCorrect" class="text-2xl font-black text-emerald-600 mt-1">0</div>
        </div>
        <div class="bg-rose-50 p-3 rounded-xl border border-rose-200">
          <div class="text-xs text-rose-700 font-semibold uppercase">Incorrect</div>
          <div id="resIncorrect" class="text-2xl font-black text-rose-600 mt-1">0</div>
        </div>
        <div class="bg-slate-50 p-3 rounded-xl border border-slate-200">
          <div class="text-xs text-slate-500 font-semibold uppercase">Unattempted</div>
          <div id="resUnattempted" class="text-2xl font-black text-slate-600 mt-1">0</div>
        </div>
      </div>

      <div class="space-y-4 mb-6">
        <h3 class="text-base font-bold text-slate-800">Answer Key & Explanations</h3>
        <div id="solutionReview" class="space-y-3 max-h-60 overflow-y-auto pr-2 text-sm text-slate-700">
          <!-- Dynamic summary list -->
        </div>
      </div>

      <div class="flex justify-end gap-3 pt-3 border-t border-slate-200">
        <button onclick="closeModalAndRetake()" class="px-5 py-2.5 bg-indigo-600 hover:bg-indigo-700 text-white font-medium text-sm rounded-lg transition">
          Retake Test
        </button>
      </div>
    </div>
  </div>

  <script>
    // 100 Authentic Questions extracted directly from KEA Land Surveyor (SSLR) Paper-II (DKSHK2026 Test 1)
    const questionsData = [
      {
        id: 1,
        question: "In QGIS, which window displays the non-spatial (descriptive) data of a vector layer in rows and columns?",
        options: ["Layers panel", "Attribute table", "Browser panel", "Processing toolbox"],
        correct: 1,
        explanation: "The Attribute Table in QGIS displays tabular non-spatial attribute values where rows represent features and columns represent attributes."
      },
      {
        id: 2,
        question: "In a GIS vector data model, 'topology' refers to:",
        options: [
          "The colour scheme applied to a map layer",
          "The pixel size of a raster dataset",
          "The projection parameters of a dataset",
          "Spatial relationships such as adjacency, connectivity and containment between features"
        ],
        correct: 3,
        explanation: "Topology expresses geometrical and spatial relationships such as connectivity, adjacency, and containment among vector entities."
      },
      {
        id: 3,
        question: "Match the QGIS vector geoprocessing tools in List-I with their outputs in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I (Tool)</th><th class='border p-1'>List-II (Output)</th></tr><tr><td class='border p-1'>a. Buffer</td><td class='border p-1'>i. Merges adjacent features having the same attribute value into one</td></tr><tr><td class='border p-1'>b. Clip</td><td class='border p-1'>ii. Creates zones at a specified distance around features</td></tr><tr><td class='border p-1'>c. Dissolve</td><td class='border p-1'>iii. Keeps only the overlapping portion of both layers with attributes of both</td></tr><tr><td class='border p-1'>d. Intersection</td><td class='border p-1'>iv. Cuts the input layer to the extent of an overlay polygon</td></tr></table>",
        options: [
          "a-ii, b-iv, c-i, d-iii",
          "a-ii, b-iii, c-i, d-iv",
          "a-iv, b-ii, c-iii, d-i",
          "a-i, b-iv, c-ii, d-iii"
        ],
        correct: 0,
        explanation: "Buffer creates distance zones (ii), Clip cuts to overlay polygon (iv), Dissolve merges based on attributes (i), and Intersection preserves overlapping zones with combined attributes (iii)."
      },
      {
        id: 4,
        question: "Match the OGC request in List-I with what it returns in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I (Request)</th><th class='border p-1'>List-II (Returns)</th></tr><tr><td class='border p-1'>a. GetMap</td><td class='border p-1'>i. WCS - raster coverage data</td></tr><tr><td class='border p-1'>b. GetFeatureInfo</td><td class='border p-1'>ii. WMS - attribute information at a clicked map location</td></tr><tr><td class='border p-1'>c. DescribeFeatureType</td><td class='border p-1'>iii. WFS - the schema (structure) of a feature type</td></tr><tr><td class='border p-1'>d. GetCoverage</td><td class='border p-1'>iv. WMS - a rendered map image</td></tr></table>",
        options: [
          "a-ii, b-iv, c-iii, d-i",
          "a-iv, b-ii, c-iii, d-i",
          "a-iv, b-iii, c-ii, d-i",
          "a-i, b-ii, c-iii, d-iv"
        ],
        correct: 1,
        explanation: "GetMap returns rendered map imagery (iv), GetFeatureInfo returns attributes of clicked pixel/point (ii), DescribeFeatureType queries WFS schema (iii), and GetCoverage retrieves WCS raster data (i)."
      },
      {
        id: 5,
        question: "In a GIS used for cadastral mapping, the boundary of a land parcel is best stored as which geometry type?",
        options: ["Point", "Polygon", "Line (polyline)", "Raster cell"],
        correct: 1,
        explanation: "Cadastral parcels are closed contiguous areas requiring area/perimeter calculations, stored as Polygons."
      },
      {
        id: 6,
        question: "To speed up spatial queries on a geometry column, PostGIS normally uses which type of index?",
        options: ["GiST (R-tree based) index", "Hash index", "Bitmap index", "Full-text index"],
        correct: 0,
        explanation: "PostGIS uses Generalized Search Tree (GiST) indexing based on bounding boxes (R-tree) to rapidly filter spatial entities."
      },
      {
        id: 7,
        question: "Given below are two statements related to AutoCAD:<br><b>Statement-I:</b> The OFFSET command creates a parallel copy of a line, arc or circle at a specified distance.<br><b>Statement-II:</b> The FILLET command with radius set to zero trims or extends two lines so that they meet at a sharp corner.<br>With respect to the above statements, choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 0,
        explanation: "Both statements are correct. FILLET with radius 0 creates a clean corner by trimming or extending lines."
      },
      {
        id: 8,
        question: "Which of the following statements is/are <b>not correct</b> regarding layers in AutoCAD?<br>(a) Each layer can have its own colour, linetype and lineweight.<br>(b) Objects on a frozen layer are displayed but cannot be edited.<br>(c) Layer 0 cannot be deleted or renamed.<br>(d) Objects on a locked layer are visible but cannot be edited.",
        options: ["(b) only", "(a) and (b)", "(b) and (d)", "(c) only"],
        correct: 0,
        explanation: "Objects on a frozen layer are invisible (not displayed) and not regenerated, making (b) the only false statement."
      },
      {
        id: 9,
        question: "Match the AutoCAD function keys in List-I with their functions in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I (Key)</th><th class='border p-1'>List-II (Function)</th></tr><tr><td class='border p-1'>a. F2</td><td class='border p-1'>i. Toggles Dynamic Input on/off</td></tr><tr><td class='border p-1'>b. F3</td><td class='border p-1'>ii. Toggles Polar Tracking on/off</td></tr><tr><td class='border p-1'>c. F10</td><td class='border p-1'>iii. Opens/closes expanded command history (text window)</td></tr><tr><td class='border p-1'>d. F12</td><td class='border p-1'>iv. Toggles Object Snap (OSNAP) on/off</td></tr></table>",
        options: [
          "a-iv, b-iii, c-ii, d-i",
          "a-iii, b-iv, c-i, d-ii",
          "a-iii, b-iv, c-ii, d-i",
          "a-ii, b-iv, c-iii, d-i"
        ],
        correct: 2,
        explanation: "F2 opens the text window (iii), F3 toggles OSNAP (iv), F10 toggles Polar Tracking (ii), and F12 toggles Dynamic Input (i)."
      },
      {
        id: 10,
        question: "Which AutoCAD command measures the straight-line distance between two picked points?",
        options: ["AREA", "DIST", "ID", "LIST"],
        correct: 1,
        explanation: "The DIST command reports the true 2D/3D distance, angle, and coordinate deltas between two points."
      },
      {
        id: 11,
        question: "The native (default) file format in which an AutoCAD drawing is saved is:",
        options: [".dxf", ".dwt", ".dws", ".dwg"],
        correct: 3,
        explanation: "The native proprietary drawing database format of AutoCAD is .dwg."
      },
      {
        id: 12,
        question: "What will be the output of the following Java code?<br><pre class='bg-slate-800 text-amber-300 p-2 rounded mt-2 text-xs font-mono'>class Test {\n  public static void main(String[] args) {\n    int a = 5;\n    int b = a++ + ++a;\n    System.out.print(b);\n  }\n}</pre>",
        options: ["11", "13", "12", "10"],
        correct: 2,
        explanation: "a++ evaluates to 5 and increments a to 6. Next, ++a increments a to 7 and evaluates to 7. Hence, 5 + 7 = 12."
      },
      {
        id: 13,
        question: "Which line of the following HTML code contains an error?<br><pre class='bg-slate-800 text-amber-300 p-2 rounded mt-2 text-xs font-mono'>1. &lt;!DOCTYPE html&gt;\n2. &lt;html&gt;\n3. &lt;head&gt;&lt;title&gt;Parcel&lt;/title&gt;&lt;/head&gt;\n4. &lt;body&gt;\n5. &lt;img src=\"map.png\" alt=\"Map\"&gt;\n6. &lt;a href=\"survey.html\"&gt;Survey&lt;/b&gt;\n7. &lt;/body&gt;&lt;/html&gt;</pre>",
        options: ["Line 5", "Line 6", "Line 3", "Line 1"],
        correct: 1,
        explanation: "Line 6 opens an anchor tag `<a>` but closes it with a mismatched `</b>` tag."
      },
      {
        id: 14,
        question: "What will be the output of the Python statement: <code class='bg-slate-200 px-1 py-0.5 rounded text-sm'>print(len([3, \"GIS\", 4.5]))</code>?",
        options: ["5", "3", "1", "8"],
        correct: 1,
        explanation: "The list contains three elements: 3 (integer), \"GIS\" (string), and 4.5 (float). `len()` returns 3."
      },
      {
        id: 15,
        question: "In a field-survey mobile application, 'geo-tagging' a photograph means:",
        options: [
          "Compressing the photo to reduce its size",
          "Encrypting the photo before upload",
          "Converting the photo into a vector layer",
          "Attaching location (latitude, longitude) and time metadata to the photo"
        ],
        correct: 3,
        explanation: "Geotagging embeds geographical identification metadata (such as GPS coordinates and timestamp) into the image file."
      },
      {
        id: 16,
        question: "In the Software Development Life Cycle (SDLC), the phase in which user requirements are documented in an SRS (Software Requirements Specification) is:",
        options: ["Design", "Testing", "Requirement analysis", "Maintenance"],
        correct: 2,
        explanation: "The Requirement Analysis phase defines and documents user functional and non-functional requirements into the SRS document."
      },
      {
        id: 17,
        question: "Consider the following statements:<br><b>Statement-I:</b> SOAP messages are always formatted in XML.<br><b>Statement-II:</b> REST APIs can return data only in XML format.<br>Choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 2,
        explanation: "SOAP strictly relies on XML messaging. REST is format-agnostic and commonly returns JSON, XML, HTML, or plain text."
      },
      {
        id: 18,
        question: "Arrange the following SDLC phases in the correct order:<br>(a) Testing<br>(b) Design<br>(c) Requirement analysis<br>(d) Deployment<br>(e) Coding",
        options: [
          "(b), (c), (e), (a), (d)",
          "(c), (e), (b), (a), (d)",
          "(c), (b), (e), (a), (d)",
          "(c), (b), (a), (e), (d)"
        ],
        correct: 2,
        explanation: "Standard SDLC order: Requirement Analysis (c) -> Design (b) -> Coding (e) -> Testing (a) -> Deployment (d)."
      },
      {
        id: 19,
        question: "Arrange the stages of the Design Thinking process used in UX design in the correct order:<br>(a) Prototype<br>(b) Empathise<br>(c) Test<br>(d) Define<br>(e) Ideate",
        options: [
          "(d), (b), (e), (a), (c)",
          "(b), (d), (e), (a), (c)",
          "(b), (e), (d), (a), (c)",
          "(b), (d), (a), (e), (c)"
        ],
        correct: 1,
        explanation: "Standard 5 stages of Design Thinking: Empathise -> Define -> Ideate -> Prototype -> Test."
      },
      {
        id: 20,
        question: "A Digital Signature Certificate (DSC) used to e-sign land records primarily ensures:",
        options: [
          "Faster upload of the document to the server",
          "Compression of the document",
          "Anonymity of the person signing",
          "Authentication, integrity and non-repudiation of the document"
        ],
        correct: 3,
        explanation: "Digital signatures provide asymmetric cryptographic guarantees for authenticity, data integrity, and legal non-repudiation."
      },
      {
        id: 21,
        question: "Arrange the following steps in the correct order to construct $\\triangle ABC$ in which $AB = 5\\text{ cm}$, $\\angle A = 60^\\circ$ and $AC = 4\\text{ cm}$:<br>(a) Join B and C.<br>(b) Draw a line segment $AB = 5\\text{ cm}$.<br>(c) At A, construct $\\angle BAX = 60^\\circ$.<br>(d) With A as centre, cut $AC = 4\\text{ cm}$ on AX.",
        options: [
          "(c), (b), (d), (a)",
          "(b), (c), (d), (a)",
          "(b), (d), (c), (a)",
          "(a), (b), (c), (d)"
        ],
        correct: 1,
        explanation: "First draw base segment AB, construct angle at vertex A, mark off side length AC along ray AX, then join B and C."
      },
      {
        id: 22,
        question: "Consider the following statements:<br><b>Statement-I:</b> The centroid of a triangle divides each median in the ratio $2 : 1$ from the vertex.<br><b>Statement-II:</b> The orthocentre of an obtuse-angled triangle lies inside the triangle.<br>Choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 2,
        explanation: "Statement I is true (centroid 2:1 ratio). Statement II is false because the orthocentre of an obtuse-angled triangle lies outside the triangle."
      },
      {
        id: 23,
        question: "In $\\triangle PQR$, $\\angle Q = 90^\\circ$, $PQ = 9\\text{ cm}$ and $QR = 12\\text{ cm}$. The length of the median drawn from $Q$ to $PR$ is:",
        options: ["6 cm", "7.5 cm", "9 cm", "10.5 cm"],
        correct: 1,
        explanation: "In a right triangle, hypotenuse $PR = \\sqrt{9^2 + 12^2} = 15\\text{ cm}$. The median to the hypotenuse equals half the hypotenuse: $15 / 2 = 7.5\\text{ cm}$."
      },
      {
        id: 24,
        question: "In trapezium $ABCD$, $AB \\parallel DC$ and diagonals meet at $O$. If $AO = (3x-1)$, $OC = (5x-3)$, $BO = (2x+1)$ and $OD = (6x-5)$, then $x = $",
        options: ["1/2", "3", "1", "2"],
        correct: 3,
        explanation: "By similar triangles, $\\frac{AO}{OC} = \\frac{BO}{OD} \\implies \\frac{3x-1}{5x-3} = \\frac{2x+1}{6x-5}$. Expanding gives $(3x-1)(6x-5) = (2x+1)(5x-3) \\implies 18x^2 - 21x + 5 = 10x^2 - x - 3 \\implies 8x^2 - 20x + 8 = 0 \\implies 2x^2 - 5x + 2 = 0 \\implies x=2$ (since $x=1/2$ makes lengths zero or negative)."
      },
      {
        id: 25,
        question: "Match the quadrilateral in List-I with the property of its diagonals in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. Rectangle</td><td class='border p-1'>i. Equal and perpendicular bisectors of each other</td></tr><tr><td class='border p-1'>b. Rhombus</td><td class='border p-1'>ii. Bisect each other only</td></tr><tr><td class='border p-1'>c. Square</td><td class='border p-1'>iii. Equal and bisect each other</td></tr><tr><td class='border p-1'>d. Parallelogram</td><td class='border p-1'>iv. Perpendicular bisectors of each other, not necessarily equal</td></tr></table>",
        options: [
          "a-iii, b-iv, c-i, d-ii",
          "a-i, b-iv, c-iii, d-ii",
          "a-iii, b-ii, c-i, d-iv",
          "a-iv, b-iii, c-i, d-ii"
        ],
        correct: 0,
        explanation: "Rectangle diagonals are equal and bisect each other (iii); Rhombus diagonals are perpendicular bisectors (iv); Square diagonals are equal & perpendicular bisectors (i); Parallelogram diagonals just bisect each other (ii)."
      },
      {
        id: 26,
        question: "In $\\triangle ABC$, $DE \\parallel BC$, $AD = 4\\text{ cm}$ and $DB = 6\\text{ cm}$. The ratio of the area of $\\triangle ADE$ to the area of $\\triangle ABC$ is:",
        options: ["4 : 25", "2 : 5", "4 : 21", "16 : 36"],
        correct: 0,
        explanation: "$AB = AD + DB = 4 + 6 = 10\\text{ cm}$. The ratio of similar triangle areas is the square of the ratio of sides: $\\left(\\frac{AD}{AB}\\right)^2 = \\left(\\frac{4}{10}\\right)^2 = \\left(\\frac{2}{5}\\right)^2 = \\frac{4}{25}$."
      },
      {
        id: 27,
        question: "Match the polygon in List-I with the sum of its interior angles in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I (Polygon)</th><th class='border p-1'>List-II (Angle Sum)</th></tr><tr><td class='border p-1'>a. Pentagon</td><td class='border p-1'>i. $1080^\\circ$</td></tr><tr><td class='border p-1'>b. Hexagon</td><td class='border p-1'>ii. $540^\\circ$</td></tr><tr><td class='border p-1'>c. Octagon</td><td class='border p-1'>iii. $1440^\\circ$</td></tr><tr><td class='border p-1'>d. Decagon</td><td class='border p-1'>iv. $720^\\circ$</td></tr></table>",
        options: [
          "a-iv, b-ii, c-i, d-iii",
          "a-ii, b-iv, c-iii, d-i",
          "a-i, b-ii, c-iv, d-iii",
          "a-ii, b-iv, c-i, d-iii"
        ],
        correct: 3,
        explanation: "Sum $= (n-2) \\times 180^\\circ$. Pentagon ($n=5$): $540^\\circ$; Hexagon ($n=6$): $720^\\circ$; Octagon ($n=8$): $1080^\\circ$; Decagon ($n=10$): $1440^\\circ$."
      },
      {
        id: 28,
        question: "The 3rd term of an arithmetic progression is 12 and its 10th term is 40. The sum of its first 20 terms is:",
        options: ["800", "880", "840", "760"],
        correct: 2,
        explanation: "$a + 2d = 12$ and $a + 9d = 40 \\implies 7d = 28 \\implies d = 4, a = 4$. $S_{20} = \\frac{20}{2} [2(4) + 19(4)] = 10 [8 + 76] = 840$."
      },
      {
        id: 29,
        question: "In $\\triangle ABC$, $D$, $E$ and $F$ are midpoints of sides $BC$, $CA$ and $AB$. If the perimeter of $\\triangle DEF$ is $15\\text{ cm}$, the perimeter of $\\triangle ABC$ is:",
        options: ["7.5 cm", "45 cm", "60 cm", "30 cm"],
        correct: 3,
        explanation: "By midpoint theorem, each side of $\\triangle DEF$ is half the length of the opposite side of $\\triangle ABC$. Hence, Perimeter($\\triangle ABC$) $= 2 \\times 15 = 30\\text{ cm}$."
      },
      {
        id: 30,
        question: "Let $U = \\{1, 2, 3, 4, 5, 6, 7, 8\\}$, $A = \\{1, 2, 3, 4\\}$ and $B = \\{3, 4, 5, 6\\}$. Match List-I with List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. $A \\cup B$</td><td class='border p-1'>i. $\\{5, 6, 7, 8\\}$</td></tr><tr><td class='border p-1'>b. $A \\cap B$</td><td class='border p-1'>ii. $\\{1, 2\\}$</td></tr><tr><td class='border p-1'>c. $A - B$</td><td class='border p-1'>iii. $\\{3, 4\\}$</td></tr><tr><td class='border p-1'>d. $A'$</td><td class='border p-1'>iv. $\\{1, 2, 3, 4, 5, 6\\}$</td></tr></table>",
        options: [
          "a-iv, b-ii, c-iii, d-i",
          "a-i, b-iii, c-ii, d-iv",
          "a-iv, b-iii, c-ii, d-i",
          "a-iv, b-iii, c-i, d-ii"
        ],
        correct: 2,
        explanation: "$A \\cup B = \\{1,2,3,4,5,6\\}$ (iv), $A \\cap B = \\{3,4\\}$ (iii), $A - B = \\{1,2\\}$ (ii), $A' = \\{5,6,7,8\\}$ (i)."
      },
      {
        id: 31,
        question: "If $a + b = 10$ and $ab = 21$, then $a^2 + b^2 = $",
        options: ["58", "79", "42", "121"],
        correct: 0,
        explanation: "$a^2 + b^2 = (a+b)^2 - 2ab = 10^2 - 2(21) = 100 - 42 = 58$."
      },
      {
        id: 32,
        question: "The factors of $x^2 - 5x - 24$ are:",
        options: [
          "(x + 8)(x - 3)",
          "(x - 8)(x + 3)",
          "(x - 6)(x + 4)",
          "(x - 12)(x + 2)"
        ],
        correct: 1,
        explanation: "Numbers multiplying to -24 and adding to -5 are -8 and 3: $(x - 8)(x + 3)$."
      },
      {
        id: 33,
        question: "Consider the following statements:<br><b>Statement-I:</b> ${}^8P_2 = 56$<br><b>Statement-II:</b> ${}^nC_r = {}^nC_{n-r}$<br>Choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 0,
        explanation: "${}^8P_2 = 8 \\times 7 = 56$ (True). Combinations formula property: ${}^nC_r = {}^nC_{n-r}$ (True)."
      },
      {
        id: 34,
        question: "The HCF of two numbers is 12 and their LCM is 360. If one of the numbers is 72, the other is:",
        options: ["48", "36", "90", "60"],
        correct: 3,
        explanation: "Product of numbers $= \\text{HCF} \\times \\text{LCM} \\implies 72 \\times x = 12 \\times 360 \\implies x = 4320 / 72 = 60$."
      },
      {
        id: 35,
        question: "For a moderately skewed distribution, the mean is 40 and the median is 38. Using the empirical relation, the mode is:",
        options: ["34", "36", "42", "44"],
        correct: 0,
        explanation: "Empirical relationship: $\\text{Mode} = 3(\\text{Median}) - 2(\\text{Mean}) = 3(38) - 2(40) = 114 - 80 = 34$."
      },
      {
        id: 36,
        question: "If $A = \\begin{bmatrix} 1 & -2 \\\\ 0 & -1 \\end{bmatrix}$, $B = \\begin{bmatrix} 1 & -4 \\\\ 3 & 5 \\end{bmatrix}$, and $3X - 2A = B$, then $X = $",
        options: [
          "\\begin{bmatrix} 1 & 0 \\\\ 1 & -1 \\end{bmatrix}",
          "\\begin{bmatrix} 3 & 0 \\\\ 3 & 3 \\end{bmatrix}",
          "\\begin{bmatrix} 1 & -8/3 \\\\ 1 & 1 \\end{bmatrix}",
          "\\begin{bmatrix} 1 & -8/3 \\\\ 1 & 7/3 \\end{bmatrix}"
        ],
        correct: 2,
        explanation: "$3X = B + 2A = \\begin{bmatrix} 1 & -4 \\\\ 3 & 5 \\end{bmatrix} + \\begin{bmatrix} 2 & -4 \\\\ 0 & -2 \\end{bmatrix} = \\begin{bmatrix} 3 & -8 \\\\ 3 & 3 \\end{bmatrix} \\implies X = \\begin{bmatrix} 1 & -8/3 \\\\ 1 & 1 \\end{bmatrix}$."
      },
      {
        id: 37,
        question: "The radius of a circle is 5 cm. The length of its longest chord is:",
        options: ["5 cm", "10 cm", "25 cm", "7.5 cm"],
        correct: 1,
        explanation: "The longest chord of a circle is its diameter $= 2r = 2 \\times 5 = 10\\text{ cm}$."
      },
      {
        id: 38,
        question: "The smallest number which, when divided by 6, 8 and 12, leaves a remainder of 5 in each case is:",
        options: ["24", "29", "53", "77"],
        correct: 1,
        explanation: "$\\text{LCM}(6, 8, 12) = 24$. Smallest number $= \\text{LCM} + \\text{Remainder} = 24 + 5 = 29$."
      },
      {
        id: 39,
        question: "Which of the following points lies on the line $2x - y = 4$?",
        options: ["(3, 2)", "(1, 2)", "(2, 1)", "(0, 4)"],
        correct: 0,
        explanation: "Substitute $(3, 2)$: $2(3) - 2 = 6 - 2 = 4$, which satisfies the equation."
      },
      {
        id: 40,
        question: "The diagonals of a rhombus:",
        options: [
          "Bisect each other at right angles",
          "Are always equal",
          "Are parallel to each other",
          "Never bisect each other"
        ],
        correct: 0,
        explanation: "A fundamental property of a rhombus is that its diagonals bisect each other perpendicularly ($90^\\circ$)."
      },
      {
        id: 41,
        question: "Match the type of matrix in List-I with the example in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. Square matrix</td><td class='border p-1'>i. $\\begin{bmatrix} 0 & 0 \\\\ 0 & 0 \\end{bmatrix}$</td></tr><tr><td class='border p-1'>b. Null matrix</td><td class='border p-1'>ii. $\\begin{bmatrix} 3 & 0 \\\\ 0 & 3 \\end{bmatrix}$</td></tr><tr><td class='border p-1'>c. Scalar matrix</td><td class='border p-1'>iii. $[1 \\ 2 \\ 3]$</td></tr><tr><td class='border p-1'>d. Row matrix</td><td class='border p-1'>iv. $\\begin{bmatrix} 1 & 2 \\\\ 3 & 4 \\end{bmatrix}$</td></tr></table>",
        options: [
          "a-ii, b-i, c-iv, d-iii",
          "a-iv, b-ii, c-i, d-iii",
          "a-iv, b-i, c-ii, d-iii",
          "a-iii, b-i, c-ii, d-iv"
        ],
        correct: 2,
        explanation: "Square matrix $\\begin{bmatrix}1&2\\\\3&4\\end{bmatrix}$ (iv), Null matrix (i), Scalar matrix (ii), Row matrix (iii)."
      },
      {
        id: 42,
        question: "In the trapezium $ABCD$, $AB \\parallel DC$, $AB = 12\\text{ cm}$ and $DC = 8\\text{ cm}$. $E$ and $F$ are midpoints of non-parallel sides $AD$ and $BC$. The length of $EF$ is:",
        options: ["10 cm", "20 cm", "4 cm", "6 cm"],
        correct: 0,
        explanation: "The mid-segment of a trapezoid is the arithmetic mean of the parallel bases: $EF = \\frac{AB + DC}{2} = \\frac{12 + 8}{2} = 10\\text{ cm}$."
      },
      {
        id: 43,
        question: "Match List-I with List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. $\\sqrt{1764}$</td><td class='border p-1'>i. 0.2</td></tr><tr><td class='border p-1'>b. $\\sqrt[3]{1331}$</td><td class='border p-1'>ii. 11</td></tr><tr><td class='border p-1'>c. $\\sqrt{0.0081}$</td><td class='border p-1'>iii. 0.09</td></tr><tr><td class='border p-1'>d. $\\sqrt[3]{0.008}$</td><td class='border p-1'>iv. 42</td></tr></table>",
        options: [
          "a-iv, b-ii, c-i, d-iii",
          "a-ii, b-iv, c-iii, d-i",
          "a-iv, b-iii, c-ii, d-i",
          "a-iv, b-ii, c-iii, d-i"
        ],
        correct: 3,
        explanation: "$\\sqrt{1764} = 42$, $\\sqrt[3]{1331} = 11$, $\\sqrt{0.0081} = 0.09$, $\\sqrt[3]{0.008} = 0.2$."
      },
      {
        id: 44,
        question: "The area of a rhombus is $120\\text{ cm}^2$ and one of its diagonals is $24\\text{ cm}$. The length of each side of the rhombus is:",
        options: ["10 cm", "13 cm", "12 cm", "17 cm"],
        correct: 1,
        explanation: "Area $= \\frac{1}{2} d_1 d_2 \\implies 120 = \\frac{1}{2}(24) d_2 \\implies d_2 = 10\\text{ cm}$. Semi-diagonals are 12 and 5. Side $= \\sqrt{12^2 + 5^2} = 13\\text{ cm}$."
      },
      {
        id: 45,
        question: "The number of lateral (triangular) faces of a hexagonal pyramid is:",
        options: ["7", "12", "6", "8"],
        correct: 2,
        explanation: "A pyramid with an $n$-sided base has exactly $n$ lateral triangular faces. For a hexagonal base ($n=6$), there are 6 lateral faces."
      },
      {
        id: 46,
        question: "The parabola $y = f(x)$ cuts the X-axis at $x = -2$ and $x = 1$ and opens upward. The corresponding quadratic equation is:",
        options: [
          "x^2 + x - 2 = 0",
          "x^2 - x - 2 = 0",
          "x^2 + x + 2 = 0",
          "x^2 - x + 2 = 0"
        ],
        correct: 0,
        explanation: "Roots are $-2$ and $1$: $(x - (-2))(x - 1) = (x + 2)(x - 1) = x^2 + x - 2 = 0$."
      },
      {
        id: 47,
        question: "The area of a parallelogram whose base is $15\\text{ cm}$ and corresponding height is $8\\text{ cm}$ is:",
        options: ["60 cm²", "46 cm²", "120 cm²", "240 cm²"],
        correct: 2,
        explanation: "Area of parallelogram $= \\text{base} \\times \\text{height} = 15 \\times 8 = 120\\text{ cm}^2$."
      },
      {
        id: 48,
        question: "The angles of a quadrilateral are $x$, $2x$, $3x$ and $4x$. Its largest angle is:",
        options: ["108°", "144°", "120°", "36°"],
        correct: 1,
        explanation: "Sum of angles $= x + 2x + 3x + 4x = 10x = 360^\\circ \\implies x = 36^\\circ$. Largest angle $= 4x = 4(36^\\circ) = 144^\\circ$."
      },
      {
        id: 49,
        question: "A ladder 13 m long reaches a window 12 m above the ground. How far is the foot of the ladder from the wall?",
        options: ["7 m", "5 m", "6 m", "4 m"],
        correct: 1,
        explanation: "By Pythagoras theorem, $\\text{Distance} = \\sqrt{13^2 - 12^2} = \\sqrt{169 - 144} = \\sqrt{25} = 5\\text{ m}$."
      },
      {
        id: 50,
        question: "In how many ways can 3 surveyors be selected from a group of 7?",
        options: ["35", "210", "21", "42"],
        correct: 0,
        explanation: "${}^7C_3 = \\frac{7 \\times 6 \\times 5}{3 \\times 2 \\times 1} = 35$."
      },
      {
        id: 51,
        question: "Match List-I with List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. $(x+4)^2$</td><td class='border p-1'>i. $x^2 - 16$</td></tr><tr><td class='border p-1'>b. $(x-4)^2$</td><td class='border p-1'>ii. $x^2 + 5x + 4$</td></tr><tr><td class='border p-1'>c. $(x+4)(x-4)$</td><td class='border p-1'>iii. $x^2 + 8x + 16$</td></tr><tr><td class='border p-1'>d. $(x+4)(x+1)$</td><td class='border p-1'>iv. $x^2 - 8x + 16$</td></tr></table>",
        options: [
          "a-iv, b-iii, c-i, d-ii",
          "a-iii, b-iv, c-i, d-ii",
          "a-iii, b-iv, c-ii, d-i",
          "a-ii, b-iv, c-i, d-iii"
        ],
        correct: 1,
        explanation: "$(x+4)^2 = x^2 + 8x + 16$ (iii); $(x-4)^2 = x^2 - 8x + 16$ (iv); $(x+4)(x-4) = x^2 - 16$ (i); $(x+4)(x+1) = x^2 + 5x + 4$ (ii)."
      },
      {
        id: 52,
        question: "In a cyclic quadrilateral $ABCD$, $\\angle A = (2x + 4)^\\circ$ and $\\angle C = (4x - 4)^\\circ$. The measure of $\\angle C$ is:",
        options: ["64°", "124°", "56°", "116°"],
        correct: 3,
        explanation: "Opposite angles sum to $180^\\circ$: $(2x + 4) + (4x - 4) = 180 \\implies 6x = 180 \\implies x = 30$. Hence, $\\angle C = 4(30) - 4 = 116^\\circ$."
      },
      {
        id: 53,
        question: "PA and PB are tangents drawn from an external point P to a circle with centre O. If $\\angle APB = 50^\\circ$, then $\\angle AOB = $",
        options: ["50°", "130°", "100°", "140°"],
        correct: 1,
        explanation: "Tangents are perpendicular to radii at points of contact. In quadrilateral $OAPB$, $\\angle AOB = 180^\\circ - 50^\\circ = 130^\\circ$."
      },
      {
        id: 54,
        question: "Arrange the following in increasing order of their dimensions:<br>(a) Surface<br>(b) Point<br>(c) Solid<br>(d) Line",
        options: [
          "(d), (b), (a), (c)",
          "(b), (a), (d), (c)",
          "(b), (d), (a), (c)",
          "(c), (a), (d), (b)"
        ],
        correct: 2,
        explanation: "Point (0D) -> Line (1D) -> Surface (2D) -> Solid (3D)."
      },
      {
        id: 55,
        question: "Which of the following are empty sets?<br>(a) $\\{x : x\\text{ is a natural number less than 1}\\}$<br>(b) $\\{x : x\\text{ is an even prime number}\\}$<br>(c) $\\{x : x^2 = 4\\text{ and }x\\text{ is an odd number}\\}$<br>(d) $\\{x : x\\text{ is a whole number less than 1}\\}$",
        options: ["(a) and (c)", "(b) and (d)", "(a), (c) and (d)", "(a) only"],
        correct: 0,
        explanation: "(a) Natural numbers start at 1 (empty set). (b) Contains {2} (non-empty). (c) Roots of $x^2=4$ are $\\pm 2$, neither is odd (empty set). (d) Contains {0} (non-empty)."
      },
      {
        id: 56,
        question: "The point of intersection of the perpendicular bisectors of the sides of a triangle is called the:",
        options: ["Incentre", "Circumcentre", "Centroid", "Orthocentre"],
        correct: 1,
        explanation: "Perpendicular bisectors meet at the Circumcentre (centre of circumscribed circle)."
      },
      {
        id: 57,
        question: "The number of vertices and edges of a square pyramid are respectively:",
        options: ["4 and 8", "5 and 6", "8 and 5", "5 and 8"],
        correct: 3,
        explanation: "A square pyramid has 4 base vertices + 1 apex = 5 vertices, and 4 base edges + 4 slant edges = 8 edges."
      },
      {
        id: 58,
        question: "Arrange the following algebraic expressions in ascending order of their degree:<br>(a) $5x^3 - 2x$<br>(b) $7$<br>(c) $x^2 y^3 + 1$<br>(d) $4x - 9$",
        options: [
          "(d), (b), (a), (c)",
          "(b), (d), (c), (a)",
          "(c), (a), (d), (b)",
          "(b), (d), (a), (c)"
        ],
        correct: 3,
        explanation: "Degree of constant 7 is 0; degree of $4x-9$ is 1; degree of $5x^3-2x$ is 3; degree of $x^2 y^3$ is $2+3=5$. Order: (b), (d), (a), (c)."
      },
      {
        id: 59,
        question: "The sum of the present ages of a father and his son is 50 years. Five years ago, the father was 7 times as old as the son. The present age of the son is:",
        options: ["12 years", "8 years", "10 years", "15 years"],
        correct: 2,
        explanation: "Let son's age be $S$, father's age is $50-S$. Five years ago: $(50 - S - 5) = 7(S - 5) \\implies 45 - S = 7S - 35 \\implies 8S = 80 \\implies S = 10$."
      },
      {
        id: 60,
        question: "In parallelogram $ABCD$, $\\angle A = (3x - 20)^\\circ$ and $\\angle B = (2x + 50)^\\circ$. The measure of $\\angle C$ is:",
        options: ["110°", "30°", "70°", "90°"],
        correct: 2,
        explanation: "Adjacent angles are supplementary: $(3x - 20) + (2x + 50) = 180 \\implies 5x + 30 = 180 \\implies 5x = 150 \\implies x = 30^\\circ$. Opposite angles are equal: $\\angle C = \\angle A = 3(30) - 20 = 70^\\circ$."
      },
      {
        id: 61,
        question: "The SI unit of magnetic flux density (magnetic field B) and its equivalent are:",
        options: [
          "Weber, equal to T/m²",
          "Gauss, equal to Wb·m²",
          "Tesla, equal to Wb·m²",
          "Tesla, equal to Wb/m²"
        ],
        correct: 3,
        explanation: "Magnetic flux density is measured in Tesla (T), which is dimensionally equivalent to Weber per square metre ($1\\text{ T} = 1\\text{ Wb}/\\text{m}^2$)."
      },
      {
        id: 62,
        question: "A straight current-carrying conductor is placed in a uniform magnetic field. The force on it is maximum when the angle between the conductor and the field is:",
        options: ["0°", "45°", "180°", "90°"],
        correct: 3,
        explanation: "Magnetic Lorentz force is $F = B I L \\sin\\theta$. It reaches maximum value when $\\sin\\theta = 1$, i.e., $\\theta = 90^\\circ$."
      },
      {
        id: 63,
        question: "Arrange the stages of a radio receiver in the order in which the signal passes through them:<br>(a) Loudspeaker<br>(b) Antenna<br>(c) Detector (demodulator)<br>(d) Tuner (RF stage)<br>(e) Audio amplifier",
        options: [
          "(b), (c), (d), (e), (a)",
          "(d), (b), (c), (e), (a)",
          "(b), (d), (e), (c), (a)",
          "(b), (d), (c), (e), (a)"
        ],
        correct: 3,
        explanation: "Signal pathway: Antenna -> RF Tuner/Amplifier -> Detector/Demodulator -> Audio Amplifier -> Loudspeaker."
      },
      {
        id: 64,
        question: "Match the physical quantity in List-I with its unit in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. Electric potential</td><td class='border p-1'>i. Kilowatt-hour</td></tr><tr><td class='border p-1'>b. Commercial electric energy</td><td class='border p-1'>ii. Volt</td></tr><tr><td class='border p-1'>c. Resistance</td><td class='border p-1'>iii. Coulomb</td></tr><tr><td class='border p-1'>d. Electric charge</td><td class='border p-1'>iv. Ohm</td></tr></table>",
        options: [
          "a-i, b-ii, c-iv, d-iii",
          "a-ii, b-i, c-iv, d-iii",
          "a-ii, b-i, c-iii, d-iv",
          "a-iv, b-i, c-ii, d-iii"
        ],
        correct: 1,
        explanation: "Potential: Volt (ii); Commercial Energy: kWh (i); Resistance: Ohm (iv); Charge: Coulomb (iii)."
      },
      {
        id: 65,
        question: "Match the radiation in List-I with its use in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. Microwaves</td><td class='border p-1'>i. Detecting forged currency notes</td></tr><tr><td class='border p-1'>b. Infrared rays</td><td class='border p-1'>ii. Radar and satellite communication</td></tr><tr><td class='border p-1'>c. Ultraviolet rays</td><td class='border p-1'>iii. Night-vision devices and TV remote controls</td></tr><tr><td class='border p-1'>d. Gamma rays</td><td class='border p-1'>iv. Radiotherapy for cancer</td></tr></table>",
        options: [
          "a-iii, b-ii, c-i, d-iv",
          "a-ii, b-iii, c-iv, d-i",
          "a-ii, b-iii, c-i, d-iv",
          "a-ii, b-i, c-iii, d-iv"
        ],
        correct: 2,
        explanation: "Microwaves for radar/satellites (ii); Infrared for night-vision/remotes (iii); UV for forgery detection (i); Gamma for cancer radiotherapy (iv)."
      },
      {
        id: 66,
        question: "In Raman scattering, the spectral lines having a wavelength longer than that of the incident light are called:",
        options: ["Anti-Stokes lines", "Stokes lines", "Rayleigh lines", "Fraunhofer lines"],
        correct: 1,
        explanation: "Stokes lines have lower frequency and longer wavelength than incident light (scattered photon loses energy to molecule)."
      },
      {
        id: 67,
        question: "Consider the following statements about the acceleration due to gravity (g):<br>(a) g is maximum at the poles.<br>(b) g decreases with depth below the Earth's surface.<br>(c) g is zero at the centre of the Earth.<br>(d) g increases with altitude above the Earth's surface.<br>Which of the above statements are correct?",
        options: ["(a) and (d)", "(b) and (c) only", "(a), (b), (c) and (d)", "(a), (b) and (c)"],
        correct: 3,
        explanation: "(a), (b), and (c) are true. Statement (d) is false because $g$ decreases with increasing height above Earth's surface: $g' \\approx g(1 - 2h/R)$."
      },
      {
        id: 68,
        question: "Which of the following are correct about ultrasonic waves?<br>(a) They are used in SONAR to measure the depth of the sea.<br>(b) They are used to detect flaws in metal castings.<br>(c) They are used in echocardiography.<br>(d) Their frequency is below 20 Hz.",
        options: ["(a) and (d)", "(b) and (d)", "(a), (b), (c) and (d)", "(a), (b) and (c)"],
        correct: 3,
        explanation: "(a), (b), and (c) are standard applications. (d) is false because ultrasonic frequencies are strictly above 20,000 Hz (20 kHz)."
      },
      {
        id: 69,
        question: "Consider the following statements:<br><b>Statement-I:</b> The time period of a simple pendulum is independent of the mass of the bob.<br><b>Statement-II:</b> The time period of a simple pendulum doubles when its length is doubled.<br>Choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 2,
        explanation: "$T = 2\\pi\\sqrt{l/g}$. $T$ is independent of mass (Statement I is true). When $l$ doubles, $T$ increases by a factor of $\\sqrt{2} \\approx 1.414$, not 2 (Statement II is false)."
      },
      {
        id: 70,
        question: "A temperature of $-40^\\circ\\text{C}$ on the Kelvin scale is approximately:",
        options: ["313 K", "-233 K", "233 K", "273 K"],
        correct: 2,
        explanation: "$T(\\text{K}) = T(^\\circ\\text{C}) + 273.15 = -40 + 273.15 = 233.15\\text{ K} \\approx 233\\text{ K}$."
      },
      {
        id: 71,
        question: "Consider the following statements:<br><b>Statement-I:</b> In a truly vertical aerial photograph, the principal point, nadir point and isocentre coincide.<br><b>Statement-II:</b> Relief displacement on a vertical photograph is radial from the principal point.<br>Choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 0,
        explanation: "Both statements are correct. When tilt angle is $0^\\circ$, nadir, isocentre, and principal point coincide, and topographic relief displacement is strictly radial from the photo centre."
      },
      {
        id: 72,
        question: "Match the photogrammetry terms in List-I with their meanings in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. Principal point</td><td class='border p-1'>i. Two overlapping photographs of the same area taken from different positions</td></tr><tr><td class='border p-1'>b. Fiducial marks</td><td class='border p-1'>ii. Marks on camera frame used to locate principal point</td></tr><tr><td class='border p-1'>c. Overlap</td><td class='border p-1'>iii. Point where optical axis meets photo plane</td></tr><tr><td class='border p-1'>d. Stereo pair</td><td class='border p-1'>iv. Common area covered by successive photographs</td></tr></table>",
        options: [
          "a-ii, b-iii, c-iv, d-i",
          "a-iii, b-ii, c-i, d-iv",
          "a-iii, b-ii, c-iv, d-i",
          "a-iv, b-ii, c-iii, d-i"
        ],
        correct: 2,
        explanation: "Principal point: intersection of optical axis (iii); Fiducials: index marks defining principal point (ii); Overlap: shared coverage (iv); Stereo pair: two overlapping views (i)."
      },
      {
        id: 73,
        question: "A vertical photograph is taken with a camera of focal length $150\\text{ mm}$ from a flying height of $2500\\text{ m}$ above MSL over terrain at $1000\\text{ m}$ above MSL. The photo scale is:",
        options: ["1 : 10,000", "1 : 16,667", "1 : 15,000", "1 : 25,000"],
        correct: 0,
        explanation: "Scale $S = \\frac{f}{H - h} = \\frac{0.150\\text{ m}}{2500 - 1000} = \\frac{0.150}{1500} = \\frac{1}{10000} = 1 : 10,000$."
      },
      {
        id: 74,
        question: "On a vertical photograph taken from $1200\\text{ m}$ above the base of a tower, the top of the tower is imaged $80\\text{ mm}$ from the principal point. If the tower is $60\\text{ m}$ high, the relief displacement is:",
        options: ["2 mm", "6 mm", "8 mm", "4 mm"],
        correct: 3,
        explanation: "Relief displacement $d = \\frac{r \\cdot h}{H} = \\frac{80\\text{ mm} \\times 60\\text{ m}}{1200\\text{ m}} = \\frac{4800}{1200} = 4\\text{ mm}$."
      },
      {
        id: 75,
        question: "In aerial photogrammetry, the usual forward (end) overlap between successive photographs along a flight line is about:",
        options: ["60%", "30%", "10%", "90%"],
        correct: 0,
        explanation: "Standard photogrammetric flight planning specifies roughly $60\\%$ forward overlap (end lap) and $20-30\\%$ side overlap (side lap) to enable continuous stereoscopic coverage."
      },
      {
        id: 76,
        question: "A Digital Terrain Model (DTM), also called a bare-earth DEM, represents:",
        options: [
          "The top surface including buildings and trees",
          "The ground surface without buildings and vegetation",
          "Only the water bodies of an area",
          "Land-use classes of an area"
        ],
        correct: 1,
        explanation: "A DTM captures the bare ground surface, stripped of non-ground objects like canopies and man-made structures (unlike a DSM)."
      },
      {
        id: 77,
        question: "Remote sensing that uses the Sun as the source of energy is called:",
        options: ["Active remote sensing", "Radar remote sensing", "Passive remote sensing", "LiDAR remote sensing"],
        correct: 2,
        explanation: "Passive remote sensing records naturally occurring reflected solar radiation or emitted thermal radiation."
      },
      {
        id: 78,
        question: "Consider the following statements:<br><b>Statement-I:</b> Spatial resolution refers to the size of the smallest object (pixel size) that a sensor can resolve on the ground.<br><b>Statement-II:</b> Temporal resolution refers to the number of spectral bands of a sensor.<br>Choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 2,
        explanation: "Statement I is correct. Statement II is incorrect because temporal resolution is revisit period/frequency; spectral resolution refers to number and width of spectral bands."
      },
      {
        id: 79,
        question: "Arrange the elements of the remote sensing process in the correct order:<br>(a) Energy source (illumination)<br>(b) Interaction with the target<br>(c) Radiation passing through the atmosphere<br>(d) Recording of energy by the sensor<br>(e) Interpretation and analysis",
        options: [
          "(a), (b), (c), (d), (e)",
          "(c), (a), (b), (d), (e)",
          "(a), (c), (d), (b), (e)",
          "(a), (c), (b), (d), (e)"
        ],
        correct: 3,
        explanation: "Energy source (a) -> Atmospheric transmission to target (c) -> Interaction with ground target (b) -> Recording by sensor (d) -> Interpretation/Analysis (e)."
      },
      {
        id: 80,
        question: "In GIS, 'overlay analysis' is used to:",
        options: [
          "Combine two or more layers to derive new information",
          "Change the map projection of a layer",
          "Scan paper maps into images",
          "Measure GNSS signal strength"
        ],
        correct: 0,
        explanation: "Overlay analysis superimposes multiple thematic spatial datasets to identify spatial intersections, unions, and create composite relationships."
      },
      {
        id: 81,
        question: "Arrange the stages of a typical GIS project in the correct order:<br>(a) Data analysis<br>(b) Data capture / input<br>(c) Output and map presentation<br>(d) Data storage and management",
        options: [
          "(d), (b), (a), (c)",
          "(b), (a), (d), (c)",
          "(b), (d), (a), (c)",
          "(b), (d), (c), (a)"
        ],
        correct: 2,
        explanation: "Data Capture/Input -> Storage & Management -> Spatial Analysis -> Visualization/Output."
      },
      {
        id: 82,
        question: "The NAVSTAR GPS satellite constellation is owned and operated by:",
        options: ["Russia", "The European Union", "India", "The United States of America"],
        correct: 3,
        explanation: "NAVSTAR GPS was developed and is operated by the United States Department of Defense/Space Force."
      },
      {
        id: 83,
        question: "Which GNSS error is largely eliminated by using dual-frequency receivers?",
        options: ["Multipath error", "Ionospheric delay", "Receiver noise", "Satellite orbit (ephemeris) error"],
        correct: 1,
        explanation: "Because the ionosphere is dispersive, receiving signals on two separate carrier frequencies (e.g. L1 & L2) allows the first-order ionospheric group delay to be directly calculated and cancelled."
      },
      {
        id: 84,
        question: "Consider the following statements:<br><b>Statement-I:</b> In RTK surveying, a base receiver on a known point sends real-time corrections to the rover.<br><b>Statement-II:</b> RTK positioning is based only on code (pseudorange) measurements.<br>Choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 2,
        explanation: "Statement I is true. Statement II is false because Real-Time Kinematic (RTK) positioning is based on carrier phase measurements with solved integer ambiguities to achieve centimetre precision."
      },
      {
        id: 85,
        question: "Corrections from the Karnataka CORS network are usually streamed to field rovers over the internet using which protocol?",
        options: ["NTRIP", "SMTP", "FTP", "POP3"],
        correct: 0,
        explanation: "NTRIP (Networked Transport of RTCM via Internet Protocol) is the standard protocol for streaming differential GNSS/RTK correction data over the internet."
      },
      {
        id: 86,
        question: "Match the satellite navigation system in List-I with the country/agency in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. GLONASS</td><td class='border p-1'>i. China</td></tr><tr><td class='border p-1'>b. Galileo</td><td class='border p-1'>ii. India</td></tr><tr><td class='border p-1'>c. BeiDou</td><td class='border p-1'>iii. Russia</td></tr><tr><td class='border p-1'>d. NavIC</td><td class='border p-1'>iv. European Union</td></tr></table>",
        options: [
          "a-iii, b-iv, c-i, d-ii",
          "a-iv, b-iii, c-i, d-ii",
          "a-iii, b-iv, c-ii, d-i",
          "a-i, b-iv, c-iii, d-ii"
        ],
        correct: 0,
        explanation: "GLONASS: Russia (iii); Galileo: European Union (iv); BeiDou: China (i); NavIC (IRNSS): India (ii)."
      },
      {
        id: 87,
        question: "A PDOP value of about 1.5 during a GNSS survey indicates:",
        options: ["Good satellite geometry", "Poor satellite geometry", "Failure of a satellite", "Heavy multipath at the site"],
        correct: 0,
        explanation: "PDOP $\\le 2$ indicates an excellent, widely distributed satellite geometry yielding high 3D positional precision."
      },
      {
        id: 88,
        question: "Arrange the steps of an RTK-based cadastral survey in the correct order:<br>(a) Set up the base receiver on a known control point<br>(b) Configure the radio/internet correction link<br>(c) Occupy parcel corners with the rover and record FIXED solutions<br>(d) Download points and export them to GIS/CAD",
        options: [
          "(b), (a), (c), (d)",
          "(a), (c), (b), (d)",
          "(a), (b), (c), (d)",
          "(c), (a), (b), (d)"
        ],
        correct: 2,
        explanation: "Base setup (a) -> Data link setup (b) -> Collect corner coordinates with rover (c) -> Export to GIS/CAD (d)."
      },
      {
        id: 89,
        question: "Match the positioning method in List-I with its typical horizontal accuracy in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. Standalone (autonomous) GPS</td><td class='border p-1'>i. A few millimetres</td></tr><tr><td class='border p-1'>b. Code-based DGPS</td><td class='border p-1'>ii. 1-2 cm</td></tr><tr><td class='border p-1'>c. RTK</td><td class='border p-1'>iii. Sub-metre to about 1 m</td></tr><tr><td class='border p-1'>d. Static post-processed baseline</td><td class='border p-1'>iv. About 5-10 m</td></tr></table>",
        options: [
          "a-iii, b-iv, c-ii, d-i",
          "a-iv, b-iii, c-i, d-ii",
          "a-iv, b-ii, c-iii, d-i",
          "a-iv, b-iii, c-ii, d-i"
        ],
        correct: 3,
        explanation: "Autonomous GPS: 5-10 m (iv); Code DGPS: sub-meter to 1 m (iii); RTK: 1-2 cm (ii); Static GNSS baseline: few mm (i)."
      },
      {
        id: 90,
        question: "Which of the following is <b>not</b> a GNSS observable directly measured by a receiver to compute position?",
        options: ["Pseudorange", "Carrier phase", "Doppler shift", "Satellite azimuth"],
        correct: 3,
        explanation: "Satellite azimuth is computed mathematically from the ephemeris data and user approximate coordinates; it is not a direct GNSS signal observable like pseudorange or carrier phase."
      },
      {
        id: 91,
        question: "The river Tungabhadra is a major tributary of which river?",
        options: ["Krishna", "Godavari", "Kaveri", "Pennar"],
        correct: 0,
        explanation: "The Tungabhadra River, formed by the confluence of Tunga and Bhadra, flows into the Krishna River near Alampur."
      },
      {
        id: 92,
        question: "Which gap in the Western Ghats provides the principal transport corridor connecting Kerala and Tamil Nadu?",
        options: ["Bhor Ghat", "Thal Ghat", "Palghat (Palakkad) Gap", "Shipki La"],
        correct: 2,
        explanation: "The Palghat (Palakkad) Gap is a low mountain pass in the Western Ghats connecting Coimbatore (TN) with Palakkad (Kerala)."
      },
      {
        id: 93,
        question: "The Thar Desert lies predominantly in the state of:",
        options: ["Gujarat", "Punjab", "Haryana", "Rajasthan"],
        correct: 3,
        explanation: "Roughly $85\\%$ of the Thar Desert is located within India, of which the vast majority lies in Rajasthan."
      },
      {
        id: 94,
        question: "Consider the following statements:<br><b>Statement-I:</b> The Western Ghats are higher and more continuous than the Eastern Ghats.<br><b>Statement-II:</b> The Godavari is the longest river of peninsular India.<br>Choose the correct answer:",
        options: [
          "Both Statement I and Statement II are correct",
          "Both Statement I and Statement II are incorrect",
          "Statement I is correct but Statement II is incorrect",
          "Statement I is incorrect but Statement II is correct"
        ],
        correct: 0,
        explanation: "Both statements are geographically accurate. The Western Ghats form an unbroken escarpment, and the Godavari (1465 km) is peninsular India's longest river."
      },
      {
        id: 95,
        question: "Match the lake in List-I with its state/UT in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. Wular</td><td class='border p-1'>i. Odisha</td></tr><tr><td class='border p-1'>b. Loktak</td><td class='border p-1'>ii. Rajasthan</td></tr><tr><td class='border p-1'>c. Chilika</td><td class='border p-1'>iii. Jammu & Kashmir</td></tr><tr><td class='border p-1'>d. Sambhar</td><td class='border p-1'>iv. Manipur</td></tr></table>",
        options: [
          "a-iv, b-iii, c-i, d-ii",
          "a-iii, b-iv, c-i, d-ii",
          "a-iii, b-iv, c-ii, d-i",
          "a-iii, b-i, c-iv, d-ii"
        ],
        correct: 1,
        explanation: "Wular: J&K (iii); Loktak: Manipur (iv); Chilika: Odisha (i); Sambhar: Rajasthan (ii)."
      },
      {
        id: 96,
        question: "Compared with a map of scale 1 : 1,000,000, a map of scale 1 : 10,000 is a:",
        options: [
          "Smaller-scale map showing more area",
          "Larger-scale map showing more detail",
          "Thematic map",
          "Globe"
        ],
        correct: 1,
        explanation: "A fraction of $1/10,000$ is larger than $1/1,000,000$, representing a large-scale map that portrays features in high detail over a smaller area."
      },
      {
        id: 97,
        question: "Match the colour used on Survey of India topographic sheets in List-I with the feature it shows in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I (Colour)</th><th class='border p-1'>List-II (Feature)</th></tr><tr><td class='border p-1'>a. Blue</td><td class='border p-1'>i. Contours</td></tr><tr><td class='border p-1'>b. Green</td><td class='border p-1'>ii. Cultivated land</td></tr><tr><td class='border p-1'>c. Brown</td><td class='border p-1'>iii. Water bodies</td></tr><tr><td class='border p-1'>d. Yellow</td><td class='border p-1'>iv. Forest / vegetation</td></tr></table>",
        options: [
          "a-iii, b-ii, c-i, d-iv",
          "a-iii, b-iv, c-i, d-ii",
          "a-iv, b-iii, c-i, d-ii",
          "a-i, b-iv, c-iii, d-ii"
        ],
        correct: 1,
        explanation: "SOI convention: Blue = water bodies (iii); Green = forests/woodland (iv); Brown = contours & sand dunes (i); Yellow = cultivated agricultural area (ii)."
      },
      {
        id: 98,
        question: "Match the rock in List-I with its type in List-II:<br><br><table class='w-full text-sm border-collapse border border-slate-300 my-2'><tr class='bg-slate-100'><th class='border p-1'>List-I</th><th class='border p-1'>List-II</th></tr><tr><td class='border p-1'>a. Granite</td><td class='border p-1'>i. Metamorphic</td></tr><tr><td class='border p-1'>b. Limestone</td><td class='border p-1'>ii. Intrusive igneous</td></tr><tr><td class='border p-1'>c. Marble</td><td class='border p-1'>iii. Sedimentary</td></tr><tr><td class='border p-1'>d. Basalt</td><td class='border p-1'>iv. Extrusive igneous</td></tr></table>",
        options: [
          "a-iv, b-iii, c-i, d-ii",
          "a-ii, b-i, c-iii, d-iv",
          "a-ii, b-iii, c-iv, d-i",
          "a-ii, b-iii, c-i, d-iv"
        ],
        correct: 3,
        explanation: "Granite: Plutonic/Intrusive igneous (ii); Limestone: Sedimentary (iii); Marble: Metamorphic (i); Basalt: Volcanic/Extrusive igneous (iv)."
      },
      {
        id: 99,
        question: "The partly molten, plastic layer of the upper mantle, which is the main source of magma, is the:",
        options: ["Lithosphere", "Inner core", "Mesosphere", "Asthenosphere"],
        correct: 3,
        explanation: "The asthenosphere (extending from roughly 80 to 200 km depth) is ductile and semi-fluid, acting as the primary source region for magma generation."
      },
      {
        id: 100,
        question: "The difference in local solar time corresponding to $1^\\circ$ of longitude is:",
        options: ["4 minutes", "1 hour", "15 minutes", "1 minute"],
        correct: 0,
        explanation: "Earth rotates $360^\\circ$ in 24 hours (1440 minutes). Hence, $1^\\circ = 1440 / 360 = 4\\text{ minutes}$."
      }
    ];

    // State
    let currentIndex = 0;
    const userAnswers = new Array(questionsData.length).fill(null);
    const markedForReview = new Array(questionsData.length).fill(false);
    let secondsRemaining = 120 * 60; // 2 hours
    let timerInterval = null;
    let examSubmitted = false;

    // Initialization
    window.addEventListener('DOMContentLoaded', () => {
      document.getElementById('totalQNum').innerText = questionsData.length;
      buildPalette();
      loadQuestion(0);
      startTimer();
      updatePaletteCounters();
    });

    // Timer Logic
    function startTimer() {
      timerInterval = setInterval(() => {
        if (secondsRemaining <= 0) {
          clearInterval(timerInterval);
          submitExam();
          alert("Time's up! Your examination paper has been submitted automatically.");
          return;
        }
        secondsRemaining--;
        const hours = Math.floor(secondsRemaining / 3600);
        const mins = Math.floor((secondsRemaining % 3600) / 60);
        const secs = secondsRemaining % 60;
        document.getElementById('timerDisplay').innerText = 
          `${String(hours).padStart(2, '0')}:${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
      }, 1000);
    }

    // Build Palette
    function buildPalette() {
      const palette = document.getElementById('paletteGrid');
      palette.innerHTML = '';
      questionsData.forEach((q, idx) => {
        const btn = document.createElement('button');
        btn.id = `palette-btn-${idx}`;
        btn.innerText = idx + 1;
        btn.className = "h-8 w-8 text-xs font-bold rounded flex items-center justify-center border transition bg-slate-100 text-slate-700 border-slate-300 hover:border-indigo-400";
        btn.onclick = () => jumpToQuestion(idx);
        palette.appendChild(btn);
      });
    }

    // Render Question
    function loadQuestion(index) {
      if (index < 0 || index >= questionsData.length) return;
      currentIndex = index;
      const q = questionsData[index];

      document.getElementById('currentQNum').innerText = index + 1;
      document.getElementById('questionText').innerHTML = q.question;

      // Render Options
      const optionsContainer = document.getElementById('optionsList');
      optionsContainer.innerHTML = '';

      q.options.forEach((optText, optIdx) => {
        const isChecked = userAnswers[index] === optIdx;
        const optWrapper = document.createElement('label');
        optWrapper.className = `flex items-start gap-3 p-3.5 rounded-xl border text-sm md:text-base cursor-pointer transition ${
          isChecked 
            ? 'bg-indigo-50 border-indigo-600 font-medium text-indigo-950 shadow-sm' 
            : 'bg-white border-slate-200 hover:bg-slate-50 text-slate-800'
        }`;

        optWrapper.innerHTML = `
          <input type="radio" name="opt" value="${optIdx}" ${isChecked ? 'checked' : ''} onchange="selectOption(${optIdx})" class="mt-1 h-4 w-4 text-indigo-600 focus:ring-indigo-500 border-slate-300">
          <span class="flex-1">${optText}</span>
        `;
        optionsContainer.appendChild(optWrapper);
      });

      // Update Navigation button states
      document.getElementById('prevBtn').disabled = (index === 0);
      document.getElementById('prevBtn').className = `px-4 py-2 text-sm font-semibold rounded-lg transition ${
        index === 0 ? 'bg-slate-100 text-slate-400 cursor-not-allowed' : 'bg-slate-200 hover:bg-slate-300 text-slate-700'
      }`;
      document.getElementById('nextBtn').innerText = (index === questionsData.length - 1) ? 'Finish' : 'Next';

      // Update Review button appearance
      const reviewBtn = document.getElementById('reviewBtn');
      if (markedForReview[index]) {
        reviewBtn.innerText = "Unmark Review";
        reviewBtn.className = "px-3 py-2 text-xs font-semibold text-white bg-amber-500 hover:bg-amber-600 rounded-lg transition";
      } else {
        reviewBtn.innerText = "Mark for Review";
        reviewBtn.className = "px-3 py-2 text-xs font-semibold text-amber-700 border border-amber-300 bg-amber-50 hover:bg-amber-100 rounded-lg transition";
      }

      updatePaletteItemStyles();
      if (window.MathJax && MathJax.typesetPromise) {
        MathJax.typesetPromise();
      }
    }

    function selectOption(optIndex) {
      if (examSubmitted) return;
      userAnswers[currentIndex] = optIndex;
      updatePaletteCounters();
      loadQuestion(currentIndex);
    }

    function clearCurrentResponse() {
      if (examSubmitted) return;
      userAnswers[currentIndex] = null;
      updatePaletteCounters();
      loadQuestion(currentIndex);
    }

    function toggleReviewFlag() {
      if (examSubmitted) return;
      markedForReview[currentIndex] = !markedForReview[currentIndex];
      updatePaletteCounters();
      loadQuestion(currentIndex);
    }

    function nextQuestion() {
      if (currentIndex < questionsData.length - 1) {
        loadQuestion(currentIndex + 1);
      } else {
        confirmSubmitTest();
      }
    }

    function prevQuestion() {
      if (currentIndex > 0) {
        loadQuestion(currentIndex - 1);
      }
    }

    function jumpToQuestion(index) {
      loadQuestion(index);
    }

    function updatePaletteItemStyles() {
      questionsData.forEach((_, idx) => {
        const btn = document.getElementById(`palette-btn-${idx}`);
        if (!btn) return;

        let baseClasses = "h-8 w-8 text-xs font-bold rounded flex items-center justify-center border transition";
        if (idx === currentIndex) {
          btn.className = `${baseClasses} ring-2 ring-indigo-600 bg-indigo-600 text-white border-transparent`;
        } else if (markedForReview[idx]) {
          btn.className = `${baseClasses} bg-amber-400 text-slate-900 border-amber-500`;
        } else if (userAnswers[idx] !== null) {
          btn.className = `${baseClasses} bg-emerald-500 text-white border-emerald-600`;
        } else {
          btn.className = `${baseClasses} bg-slate-100 text-slate-700 border-slate-300 hover:border-indigo-400`;
        }
      });
    }

    function updatePaletteCounters() {
      let answered = 0;
      let marked = 0;
      userAnswers.forEach((ans, i) => {
        if (ans !== null) answered++;
        if (markedForReview[i]) marked++;
      });
      document.getElementById('countAnswered').innerText = answered;
      document.getElementById('countUnanswered').innerText = questionsData.length - answered;
      document.getElementById('countMarked').innerText = marked;
    }

    function confirmSubmitTest() {
      let unanswered = 0;
      userAnswers.forEach(ans => { if (ans === null) unanswered++; });
      const promptMsg = unanswered > 0 
        ? `You still have ${unanswered} unanswered question(s). Are you sure you want to finish the exam?` 
        : `Are you sure you want to submit your responses?`;
      if (confirm(promptMsg)) {
        submitExam();
      }
    }

    function submitExam() {
      clearInterval(timerInterval);
      examSubmitted = true;

      let correctCount = 0;
      let incorrectCount = 0;
      let unattemptedCount = 0;

      questionsData.forEach((q, i) => {
        const ans = userAnswers[i];
        if (ans === null) {
          unattemptedCount++;
        } else if (ans === q.correct) {
          correctCount++;
        } else {
          incorrectCount++;
        }
      });

      // Score evaluation: +1 for correct, -0.25 for incorrect
      const totalScore = (correctCount * 1.0) - (incorrectCount * 0.25);

      document.getElementById('resScore').innerText = totalScore.toFixed(2);
      document.getElementById('resCorrect').innerText = correctCount;
      document.getElementById('resIncorrect').innerText = incorrectCount;
      document.getElementById('resUnattempted').innerText = unattemptedCount;

      // Populate review solutions
      const reviewContainer = document.getElementById('solutionReview');
      reviewContainer.innerHTML = '';
      questionsData.forEach((q, i) => {
        const userAns = userAnswers[i];
        const isRight = (userAns === q.correct);
        const card = document.createElement('div');
        card.className = `p-3 rounded-lg border ${
          userAns === null ? 'bg-slate-50 border-slate-200' :
          isRight ? 'bg-emerald-50/70 border-emerald-200' : 'bg-rose-50/70 border-rose-200'
        }`;
        
        card.innerHTML = `
          <div class="font-semibold text-slate-800 text-xs mb-1">Q${i+1}. ${q.question.replace(/<table[\s\S]*?<\/table>/gi, '[Table]')}</div>
          <div class="text-xs space-y-0.5">
            <div><span class="font-medium">Your Answer:</span> ${userAns !== null ? q.options[userAns] : '<span class="italic text-slate-400">Not Attempted</span>'}</div>
            <div><span class="font-medium text-emerald-700">Correct Answer:</span> ${q.options[q.correct]}</div>
            <div class="text-slate-600 mt-1"><span class="font-medium">Explanation:</span> ${q.explanation}</div>
          </div>
        `;
        reviewContainer.appendChild(card);
      });

      document.getElementById('resultModal').classList.remove('hidden');
    }

    function closeModalAndRetake() {
      document.getElementById('resultModal').classList.add('hidden');
      for (let i = 0; i < userAnswers.length; i++) {
        userAnswers[i] = null;
        markedForReview[i] = false;
      }
      secondsRemaining = 120 * 60;
      examSubmitted = false;
      currentIndex = 0;
      updatePaletteCounters();
      loadQuestion(0);
      startTimer();
    }
  </script>
</body>
</html>
```eof

### Key Highlights of the Mock Test Application:
1. **Full 120-Minute Exam Simulation**: Includes a synchronized countdown timer (`02:00:00`), live tracking of attempted, unattempted, and flagged review questions.
2. **Exact Syllabus & Document Coverage**: Contains all 100 English-medium questions covering QGIS/GIS topology, AutoCAD commands and shortcuts, Python/Java/SDLC concepts, geometry, trigonometry, algebra, basic physics, photogrammetry, remote sensing, GNSS/RTK surveying, and Karnataka/India geography.
3. **Official Marking Scheme**: Automatically computes scores using the standard KEA ratio (+1.0 mark for correct answers, -0.25 mark penalty for wrong answers).
4. **Interactive Review & Explanations**: Generates an instant performance breakdown and full answer key with pedagogical explanations once submitted.

