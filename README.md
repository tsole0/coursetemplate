# LaTeX Notes System Documentation
### NOTE: This templated was generated with the use of artificial intelligence and is not wholly my own work.
The purpose of this project was to set up a sustainable, modular, and most importantly *pretty* system for $$\LaTeX$$. Key features of the project include:
- Completely PDF/A-3 compliant for universal display
- Modular style files that simplfiy imports and minimize duplicated code
- Lightweight, course-unique style files that allow for a common theme but taylored details
- Tons of built-in math and chemistry quality of life packages that make note-taking efficient and easy-to-remember.

WARNING: These templates are intended to be compiled using **LuaLaTeX** and are untested on other distributions. PdfLaTeX is definitely not compatible with the templates, and XeLaTeX perhaps could be, but would most likely require some modifications.

---

## 🏗️ **System Architecture**

### **Four-Layer Modular Design**

```
classnotes-base.sty      ← Core infrastructure (semantic boxes, formatting)
├── classnotes-math.sty  ← Mathematics packages and environments  
├── classnotes-chem.sty  ← Chemistry packages and environments
└── course-[name].sty    ← Course-specific definitions (lightweight)
```

### **Dependency Flow**
```
Your Document
    ↓
course-specific.sty (lightweight definitions)
    ↓
subject-module.sty (math/chem/physics packages)
    ↓
classnotes-base.sty (core infrastructure)
```

---

## PDF/A Compliance Support

The modular system includes full support for PDF/A-3u compliance for long-term archival and accessibility:

### Setup

To enable PDF/A compliance in your documents:

1. **Load pdfx package first** (before any other packages):
```latex
\usepackage[a-3u]{pdfx}
```

2. **Use LuaLaTeX** with modern fonts:
```latex
\usepackage{fontspec}
\setmainfont{Charis SIL}  % Or another high-quality Unicode font
```

3. **Create XMP metadata file** (same name as document with .xmpdata extension):
```latex
% simple-modular-example.xmpdata
\Title{Your Document Title}
\Author{Your Name}
\Language{en-US}
\Subject{Document description}
\Keywords{LaTeX, class notes, PDF/A}
\Creator{LaTeX with pdfx package}
\Producer{LuaLaTeX}
\Copyright{Copyright information}
```

### Features

- **PDF/A-3u compliance**: Long-term archival standard
- **Embedded color profiles**: Ensures consistent color reproduction
- **Modern Unicode fonts**: Full character coverage and professional typography
- **Accessibility features**: Tagged PDF structure for screen readers
- **Metadata embedding**: Rich document metadata for indexing and discovery

### Example

See `simple-modular-example.tex` and its corresponding `.xmpdata` file for a complete working example of PDF/A-compliant documents using the modular system.

### Compilation

Always use LuaLaTeX for PDF/A documents:
```bash
lualatex -output-directory=out_dir your-document.tex
```

---

## Troubleshooting

### **Base Layer: `classnotes-base.sty`**
**Purpose**: Core infrastructure without subject-specific content

#### **Included Packages**
```latex
% Infrastructure
xkeyval, ifthen          % Key-value processing and conditionals
geometry                 % Page layout
microtype               % Typography enhancement
graphicx                % Image handling

% Visual Design  
xcolor                  % Color definitions
tcolorbox[theorems,skins] % Custom colored boxes with advanced styling

% Headers/Footers
fancyhdr                % Custom headers and footers
lastpage                % Page numbering (Page X of Y)

% Margin Annotations
marginnote              % Margin notes with positioning
fontawesome5            % Professional icons (⚠️ 🔬 ⭐ etc.)

% Hyperlinks
hyperref                % PDF bookmarks and cross-references
```

#### **Core Features**
- ✅ Semantic box environments (`basebox`, `notebox`, `warnbox`)
- ✅ Professional color scheme (forest green theme)
- ✅ Auto-positioning headers with course info
- ✅ Margin annotation system with FontAwesome icons
- ✅ Title page generation
- ✅ PDF/A compliance ready

#### **No Dependencies**: Pure foundational layer

---

### **Subject Modules**

#### **`classnotes-math.sty`**
**Purpose**: Mathematics-specific functionality

#### **Included Packages**
```latex
% Core Mathematics
amsmath, amsthm, amssymb % AMS math suite (equations, theorems, symbols)
mathtools               % Enhanced math features
latexsym, esint         % Additional symbols and integrals
mathrsfs, dsfont        % Script and double-struck fonts

% Graphics & Diagrams
tikz                    % Vector graphics and diagrams
pgfplots                % Data visualization and plots  
tikz-cd                 % Commutative diagrams
```

#### **Available Math Commands**
```latex
% Number Sets
\N, \Z, \Q, \R, \C, \F, \K   % Blackboard bold number sets

% Mathematical Constructs
\abs{x}                      % |x| with auto-sizing
\norm{x}                     % ||x|| with auto-sizing  
\inner{u}{v}                 % ⟨u,v⟩ inner product
\set{x | P(x)}              % {x | P(x)} with auto-sizing
\paren{expr}, \bracket{expr} % Auto-sizing parentheses/brackets

% Calculus
\dd{x}                      % dx differential
\dv{f}{x}                   % df/dx derivative
\pdv{f}{x}                  % ∂f/∂x partial derivative
\integral{a}{b}{f(x)}{x}    % ∫[a to b] f(x) dx

% Linear Algebra
\mat{A}, \vec{v}            % Bold matrices and vectors
\transpose{A}               % A^T transpose

% Common Operators
\rank, \nullity, \trace, \span, \dim  % Standard operators
\ker, \im, \coker                     % Kernel, image, cokernel
\Hom, \End, \Aut                      % Homomorphisms, endomorphisms
```

#### **Math Environments**
```latex
\begin{mathenv}{Type}{Title}     % Numbered mathematical environment
\begin{mathenvstar}{Type}{Title} % Unnumbered version
\begin{mathformula}{Title}       % Formula box with numbering
\begin{mathnote}[Title]          % Mathematical note box
\begin{mathwarning}[Title]       % Mathematical warning box
```

**Dependencies**: `classnotes-base.sty`

---

#### **`classnotes-chem.sty`**
**Purpose**: Chemistry and engineering functionality

#### **Included Packages**
```latex
% Chemistry Core
chemfig                 % Chemical structure diagrams
chemmacros             % Comprehensive chemistry macros
chemformula            % Chemical formulas with proper formatting
modiagram              % Molecular orbital diagrams

% Measurements & Units
siunitx                % SI units and scientific notation

% Engineering
circuitikz             % Circuit diagrams for engineering
pgfplots               % Data analysis and graphs
```

#### **Available Chemistry Commands**

##### **Functional Groups**
```latex
\hydroxylgroup         % -OH
\carbonylgroup         % >C=O  
\carboxylgroup         % -COOH
\aminogroup           % -NH2
\alkylgroup           % -R
\phenylgroup          % -Ph
\benzylgroup          % -Bn
```

##### **Common Molecules**
```latex
\methane              % CH4
\ethane               % C2H6  
\propane              % C3H8
\butane               % C4H10
\carbondioxide        % CO2
% Note: \water and \ammonia removed due to package conflicts
% Use \ch{H2O} and \ch{NH3} directly
```

##### **Chemical Structures**
```latex
\benzenering          % Benzene ring diagram
```

##### **Reaction Arrows & Conditions**
```latex
\reactionarrow[above][below]  % →[above][below]
\equilibrium                  % ⇌
\mesomeric                   % ↔
\heatcondition               % Δ (heat symbol)
\catalyst{reagent}           % →[reagent]
```

##### **Units & Measurements**
```latex
% Base SI Units
\meter, \kilogram, \second, \ampere, \kelvin, \mole, \candela

% Derived Units  
\newton, \pascal, \joule, \watt, \volt, \ohm, \farad, \henry

% Chemistry-Specific
\molarity             % M (molarity)
\molality             % m (molality)
\celsius              % °C (from siunitx)
```

#### **Chemistry Environments**
```latex
\begin{chemenv}{Type}{Title}      % Numbered chemistry environment
\begin{chemenvstar}{Type}{Title}  % Unnumbered version
\begin{chemmechanism}{Title}      % Reaction mechanism box
\begin{molorbital}[Title]         % Molecular orbital diagram box
\begin{chemsafety}[Title]         % Safety warning box
```

**Dependencies**: `classnotes-base.sty`

---

### **Course Layer: `course-orgchem.sty`**
**Purpose**: Lightweight course-specific definitions

#### **Named Environments**
Maps semantic environments to course-specific names:

```latex
% Academic Environments
\begin{theorem}{Title}           → mathenv
\begin{definition}{Title}        → chemenv  
\begin{lemma}{Title}            → mathenv
\begin{corollary}{Title}        → mathenv
\begin{example}[Title]          → chemenv
\begin{proof}[Title]            → baseproof

% Chemistry-Specific
\begin{chemreaction}[Title]     → chemenv
\begin{mechanism}[Title]        → chemmechanism  
\begin{modagram}[Title]         → molorbital (renamed to avoid conflicts)
\begin{formula}[Title]          → mathformula

% General Purpose
\begin{note}[Title]             → mathnote
\begin{warning}[Title]          → chemsafety
```

#### **Organic Chemistry Shortcuts**
```latex
% Common Groups (note: some removed due to conflicts)
\Et, \Me, \Bu, \Ph, \Bn         % Ethyl, Methyl, Butyl, Phenyl, Benzyl
\Ac, \Ts, \Ms                   % Acetyl, Tosyl, Mesyl

% Solvents
\THF, \DCM, \DMSO, \DMF, \EtOH, \MeOH

% Reaction Conditions
\heatarrow                      % →[Δ]
\acidarrow                      % →[H+]  
\basearrow                      % →[OH-]
```

**Dependencies**: `classnotes-base.sty`, `classnotes-chem.sty`

---

## 🎨 **Margin Symbols & Annotations**

### **Built-in Symbol Commands**
```latex
% Base symbols (from FontAwesome)
\cautionsymbol        % ⚠️ Triangle warning
\notesymbol          % ℹ️ Info circle
\warningsymbol       # ❗ Exclamation circle
\tipsymbol           # 💡 Light bulb
\questionsymbol      # ❓ Question mark

% Math-specific
\mathcautionsymbol   % ⚠️ Math warning
\importantsymbol     # ⭐ Star (important)
\keysymbol          # 🔑 Key (key concept)
\remembersymbol     # 🧠 Brain (remember)

% Chemistry-specific  
\chemsafetysymbol   # ☢️ Radiation (chemical safety)
\toxicsymbol        # ☠️ Skull (toxic)
\explosivesymbol    # 💣 Bomb (explosive)
\corrosivesymbol    # 🧪 Flask (corrosive)
\environmentalsymbol # 🍃 Leaf (environmental)
```

### **Using Margin Annotations**

#### **Simple Icon Placement**
```latex
\marginicon[offset]{symbol}     % Places icon in margin
\marginicon[0.5cm]{\cautionsymbol}   % Caution icon 0.5cm down
\marginicon[-1cm]{\importantsymbol}  % Important icon 1cm up
```

#### **Icon with Text** 
```latex
% Course-specific commands (from course-orgchem.sty)
\caution[offset]                     % Just the caution icon
\cautionnote[offset]{text}           % Icon + italic text
\safetynote[offset]{text}            % Safety icon + red bold text  
\importantnote[offset]{text}         % Star icon + bold text
\remembernote[offset]{text}          % Brain icon + italic text
```

#### **Adding Custom Margin Symbols**

**Method 1: Quick addition to course file**
```latex
% In your course-specific .sty file
\newcommand{\mynote}[2][0cm]{
  \marginicon[#1]{\questionsymbol}
  \marginnote{\small\textit{#2}}[#1]
}

% Usage
\mynote[0.5cm]{Check this later!}
```

**Method 2: Professional implementation**
```latex
% In your course-specific .sty file  
\newcommand{\conceptnote}[2][0cm]{
  \marginicon[#1]{\keysymbol}
  \marginnote{\small\textcolor{noteblue}{\textbf{Key:} #2}}[#1]
}

% Usage
\conceptnote[1cm]{This is a fundamental concept}
```

**Method 3: New symbol from FontAwesome**
```latex
% Find symbol at https://fontawesome.com/icons
% Add to course file:
\newcommand{\experimentsymbol}{\faFlask}  
\newcommand{\experimentnote}[2][0cm]{
  \marginicon[#1]{\experimentsymbol}
  \marginnote{\small\textcolor{orange}{\textbf{Experiment:} #2}}[#1]
}
```

---

## 🔧 **Creating Course-Specific Style Files**

### **Template for New Course**

Create `course-yourcourse.sty`:

```latex
\ProvidesPackage{course-yourcourse}[2025/07/23 Your Course Name]

% ============================================================================
% COURSE-SPECIFIC DEFINITIONS: YOUR COURSE NAME
% ============================================================================
% Course: Your Course Name
% Instructor: [Your Instructor]  
% Semester: [Semester Year]
% Dependencies: classnotes-base.sty, [subject-module.sty]
% ============================================================================

% Load required modules
\RequirePackage{classnotes-base}
\RequirePackage{classnotes-math}     % If math-heavy course
\RequirePackage{classnotes-chem}     % If chemistry/engineering course

% ============================================================================
% COURSE-SPECIFIC ENVIRONMENTS
% ============================================================================

% Map semantic environments to course terminology
\newenvironment{concept}[1]{
  \begin{mathenv}{Concept}{#1}
}{
  \end{mathenv}
}

\newenvironment{principle}[1]{
  \begin{chemenv}{Principle}{#1}
}{
  \end{chemenv}
}

% Examples (choose appropriate base environment)
\newenvironment{case}[1][Case Study]{
  \begin{chemenv}{Case Study}{#1}
}{
  \end{chemenv}
}

% ============================================================================
% COURSE-SPECIFIC MARGIN SYMBOLS
% ============================================================================

\newcommand{\reviewsymbol}{\faRedo}   % Review symbol
\newcommand{\reviewnote}[2][0cm]{
  \marginicon[#1]{\reviewsymbol}
  \marginnote{\small\textcolor{purple}{\textbf{Review:} #2}}[#1]
}

\newcommand{\examsymbol}{\faGraduationCap}  % Exam symbol
\newcommand{\examnote}[2][0cm]{
  \marginicon[#1]{\examsymbol}
  \marginnote{\small\textcolor{red}{\textbf{Exam:} #2}}[#1]
}

% ============================================================================
% COURSE-SPECIFIC SHORTCUTS
% ============================================================================

% Add course-specific abbreviations and commands here
\newcommand{\coursetermA}{Definition A}
\newcommand{\coursetermB}{Definition B}

% ============================================================================
% COURSE SETUP
% ============================================================================

% Convenience command for this course
\newcommand{\setupyourcourse}[2]{
  \setupnotesheader{Your Course Name}{#1}{#2}
}

\endinput
```

### **Steps to Create New Course**

1. **Copy the template** above to `course-yourname.sty`
2. **Choose subject modules**: Include `classnotes-math` and/or `classnotes-chem` as needed
3. **Define environments**: Map semantic environments to course-appropriate names
4. **Add margin symbols**: Create course-specific annotation commands
5. **Add shortcuts**: Include frequently used terms and symbols
6. **Test compilation**: Create a simple document to test your new course style

### **Subject-Specific Variations**

#### **Pure Mathematics Course**
```latex
\RequirePackage{classnotes-base}
\RequirePackage{classnotes-math}
% No chemistry module needed

\newenvironment{proposition}[1]{\begin{mathenv}{Proposition}{#1}}{\end{mathenv}}
\newenvironment{axiom}[1]{\begin{mathenvstar}{Axiom}{#1}}{\end{mathenvstar}}
```

#### **Engineering Course**  
```latex
\RequirePackage{classnotes-base}
\RequirePackage{classnotes-chem}    % For circuitikz and siunitx
\RequirePackage{classnotes-math}    % For mathematical analysis

\newenvironment{design}[1]{\begin{chemenv}{Design}{#1}}{\end{chemenv}}
\newcommand{\voltage}{\si{\volt}}
\newcommand{\current}{\si{\ampere}}
```

#### **Physics Course**
```latex
\RequirePackage{classnotes-base}
\RequirePackage{classnotes-math}    % For equations
\RequirePackage{classnotes-chem}    % For units via siunitx

\newenvironment{law}[1]{\begin{mathenv}{Law}{#1}}{\end{mathenv}}
\newcommand{\energy}{\si{\joule}}
\newcommand{\force}{\si{\newton}}
```

---

## � **Quick Start Guide**

### **Basic Document Setup**
```latex
\documentclass[12pt, a4paper]{article}

% Essential packages
\usepackage{geometry}
\usepackage[tracking=true]{microtype}
\usepackage{graphicx}

% Load your course package (auto-loads dependencies)
\usepackage{course-orgchem}  % or your custom course

% Page setup
\geometry{
  left=1.2in, right=1in, top=1.2in, bottom=1.2in,
  marginparwidth=1in, headheight=15pt
}

% Hyperref configuration  
\hypersetup{
  colorlinks=true,
  linkcolor=blue,
  urlcolor=blue,
  citecolor=blue
}

% Setup course header
\setuporgchem{Your Name}{Semester Year}

\begin{document}
\notestitlepage
\tableofcontents
\newpage

% Your content here...
\end{document}
```

### **Compilation Command**
```bash
lualatex -output-directory=out_dir filename.tex
```

### **Example Content**
```latex
\section{Topic Name}

\begin{definition}{Important Term}
This is a key definition for the course.
\end{definition}

\importantnote[0.5cm]{This will be on the exam!}

\begin{example}[Application]
Here's how to apply this concept:
\begin{itemize}
\item Step one
\item Step two  
\item Final result
\end{itemize}
\end{example}

\cautionnote[0cm]{Be careful with this common mistake!}

\begin{formula}[Key Equation]
\begin{equation}
E = mc^2
\end{equation}
\end{formula}
```

---

## ✅ **Features Summary**

### **Automatic Features**
- ✅ **Auto-numbering**: All theorem-like environments number automatically
- ✅ **Cross-references**: Use `\label{}` and `\ref{}` as usual
- ✅ **Professional styling**: Green boxes with rounded corners and shadows
- ✅ **Header/footer**: Course name, student name, date, and page numbers
- ✅ **Table of contents**: Auto-generated with clickable links
- ✅ **PDF organization**: All output files go to `out_dir/` folder

### **Available Environments**
- ✅ **Academic**: theorem, definition, lemma, corollary, example, proof
- ✅ **Chemistry**: chemreaction, mechanism, modagram
- ✅ **General**: note, warning, formula
- ✅ **Custom**: Easy to add more in course files

### **Margin System**
- ✅ **Professional icons**: FontAwesome symbols for visual appeal
- ✅ **Flexible positioning**: Control vertical offset with `[distance]`
- ✅ **Text annotations**: Combine icons with explanatory text
- ✅ **Color coordination**: Icons and text match environment themes

### **Subject Support**
- ✅ **Mathematics**: Complete AMS package suite, tikz, custom operators
- ✅ **Chemistry**: Molecular diagrams, reaction mechanisms, SI units
- ✅ **Engineering**: Circuit diagrams, professional units, safety symbols
- ✅ **Extensible**: Easy to add physics, biology, economics modules

---

## 🔧 **Advanced Customization**

### **Color Scheme Modification**
Edit colors in `classnotes-base.sty`:
```latex
% Change the primary theme colors
\definecolor{notegreen}{RGB}{34, 139, 34}      % Main box color
\definecolor{lightgreen}{RGB}{240, 255, 240}   % Background  
\definecolor{bordergreen}{RGB}{46, 125, 50}    % Border
```

### **Font Customization**
```latex
% In your document preamble
\usepackage{fontspec}  % For LuaLaTeX
\setmainfont{Times New Roman}  % Or your preferred font
```

### **Custom Box Styles**
```latex
% In course file - create new environment type
\newtcolorbox{specialbox}[2]{
  enhanced, colback=yellow!10, colframe=orange,
  coltitle=white, colbacktitle=orange,
  fonttitle=\bfseries, rounded corners,
  title={#1}, label={#2}
}
```

---

## 🎯 **Troubleshooting**

### **Common Issues**

**Environment not found**: Check that appropriate subject module is loaded
**Package conflicts**: Ensure correct loading order (base → subject → course)  
**Symbol not displaying**: Install FontAwesome package or use alternative symbol
**Compilation errors**: Use LuaLaTeX engine, not pdfLaTeX
**Margin notes overlapping**: Adjust `marginparwidth` in geometry settings

### **Debug Strategy**
1. **Compilation issues**: Check `classnotes-base.sty` loading
2. **Environment issues**: Check subject module files  
3. **Symbol issues**: Check course-specific file
4. **Layout issues**: Check geometry and margin settings

---

## 📈 **System Benefits**

### **For Students**
- Professional-looking notes that stand out
- Consistent formatting across all courses
- Easy review with color-coded environments
- Margin annotations for quick reference
- Export-ready PDFs for sharing

### **For Instructors**  
- Standardized note-taking across students
- Easy identification of key concepts
- Professional presentation for course materials
- Modular system allows course customization

### **For Developers**
- Clean separation of concerns
- Easy maintenance and debugging
- Extensible architecture for new subjects  
- Reusable components across courses
- Version control friendly (small, focused files)

---

## 🚀 **Next Steps**

1. **Start with existing course**: Use `course-orgchem.sty` as template
2. **Create your course file**: Follow the template in this documentation
3. **Test thoroughly**: Create sample documents with all environments
4. **Customize gradually**: Add symbols and shortcuts as needed
5. **Share and collaborate**: Modular design enables team development

The system is production-ready and designed for long-term use throughout your academic career!

---
