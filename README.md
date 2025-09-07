<!-- GitHub-safe HTML README -->
<h1 id="title">RAG Optimization with MongoDB: Vector Search, Metadata Filters, Reranking & Prompt Compression</h1>

<p><em>One‑line description:</em> <strong>Inside this project, semantic search results flow through metadata pre‑filters, lean projections, rerankers, and prompt compressors to slash latency & cost while boosting relevance.</strong></p>

<p>
  <a href="#getting-started">Get Started</a> ·
  <a href="#notebooks">Notebooks</a> ·
  <a href="#learning-outcomes">What You'll Learn</a> ·
  <a href="#setup">Setup</a> ·
  <a href="#usage">Usage</a> ·
  <a href="#faq">FAQ</a>
</p>

<hr/>

<h2 id="overview">Overview</h2>
<p>
This repo demonstrates practical techniques to optimize Retrieval‑Augmented Generation (RAG) on MongoDB:
<strong>vanilla vector search</strong> as a baseline; <strong>prefiltering/postfiltering</strong> with metadata; <strong>projection</strong> to trim payloads; <strong>reranking/boosting</strong> to surface the most helpful chunks; and <strong>prompt compression</strong> to cut token costs without sacrificing answer quality. Each concept is implemented as a hands‑on Jupyter notebook.
</p>

<h2 id="notebooks">Notebook Map</h2>
<ul>
  <li><code>Vanilla Vector Search.ipynb</code> — Build a baseline vector search for RAG using MongoDB (create an embedding index, insert docs, run kNN search).</li>
  <li><code>Filtering with Metadata.ipynb</code> — Apply <strong>prefiltering</strong> at query/index time (e.g., tags, source, date) and <strong>postfiltering</strong> after retrieval to enforce business rules or user scopes.</li>
  <li><code>Projections.ipynb</code> — Use <strong>projection</strong> stages to return only the fields your application needs, reducing bandwidth, memory, and exposure of sensitive data.</li>
  <li><code>Boosting.ipynb</code> — Implement <strong>reranking & score boosting</strong> using metadata features (recency, authority, doc type) to elevate high‑value results.</li>
  <li><code>Prompt Compression.ipynb</code> — Compress prompts and retrieved context to lower token counts and improve throughput while preserving answer quality.</li>
</ul>

<h2 id="learning-outcomes">What You'll Learn</h2>
<ul>
  <li>Implement vector search for RAG with MongoDB.</li>
  <li>Develop multi‑stage MongoDB aggregation pipelines.</li>
  <li>Use metadata to refine/limit search results (efficiency & relevancy).</li>
  <li>Streamline outputs with <code>$project</code> to reduce data size and improve performance, memory use, and security.</li>
  <li>Rerank documents to improve retrieval quality and leverage metadata to guide ordering.</li>
  <li>Apply prompt compression techniques and understand their operational benefits.</li>
  <li>Optimize efficiency, security, query speed, and cost in production RAG systems.</li>
</ul>

<h2 id="getting-started">Getting Started</h2>
<ol>
  <li><strong>Clone</strong>
    <pre><code>git clone &lt;YOUR_REPO_URL&gt;
cd &lt;YOUR_REPO_NAME&gt;
</code></pre>
  </li>
  <li><strong>Python environment</strong>
    <pre><code>python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
</code></pre>
  </li>
  <li><strong>Configure environment</strong>
    <p>Create a <code>.env</code> file (or set shell vars) with your MongoDB connection and, if applicable, your LLM key:</p>
    <pre><code>MONGODB_URI=mongodb+srv://...         # required
MONGODB_DB=rag_db                      # optional (default used in notebooks)
MONGODB_COLLECTION=documents           # optional (default used in notebooks)
OPENAI_API_KEY=...                    # optional, only if a notebook calls an LLM
</code></pre>
  </li>
  <li><strong>Start Jupyter</strong>
    <pre><code>jupyter lab   # or: jupyter notebook
</code></pre>
  </li>
</ol>

<h2 id="setup">MongoDB & Data Setup</h2>
<ol>
  <li>Ensure you have a MongoDB cluster (Atlas or self‑hosted) reachable via <code>MONGODB_URI</code>.</li>
  <li>Create a collection and a vector index (the notebooks show how to define the schema and index for embeddings).</li>
  <li>Load sample documents with text, embeddings, and useful metadata (e.g., <code>source</code>, <code>created_at</code>, <code>doctype</code>, <code>tags</code>).</li>
</ol>

<h2 id="usage">How to Use the Notebooks</h2>
<ol>
  <li>Run <code>Vanilla Vector Search.ipynb</code> first to validate embeddings, insert data, and perform basic kNN retrieval.</li>
  <li>Explore <code>Filtering with Metadata.ipynb</code> to compare prefiltering (query constraints / index) vs postfiltering (application‑side and pipeline‑stage filters).</li>
  <li>Use <code>Projections.ipynb</code> to trim payloads with <code>$project</code> and measure performance & memory differences.</li>
  <li>Open <code>Boosting.ipynb</code> to add reranking/boosting heuristics or scoring functions that prioritize high‑signal documents.</li>
  <li>Finish with <code>Prompt Compression.ipynb</code> to minimize tokens (e.g., context summarization, key‑sentence extraction, vocabulary compaction).</li>
</ol>

<h2 id="design-notes">Design Notes</h2>
<ul>
  <li><strong>Prefiltering vs Postfiltering</strong>: Prefilter early to shrink candidate sets (faster queries); postfilter for user‑specific rules and UI constraints.</li>
  <li><strong>Projection</strong>: Treat <code>$project</code> as a security boundary—only return what the client needs.</li>
  <li><strong>Reranking/Boosting</strong>: Blend vector score with metadata features (recency, authority, click‑through) for better relevance.</li>
  <li><strong>Prompt Compression</strong>: Compress both query and context; evaluate quality vs token savings before/after changes.</li>
</ul>

<h2 id="structure">Repo Structure</h2>
<pre><code>.
├─ notebooks/
│  ├─ Vanilla Vector Search.ipynb
│  ├─ Filtering with Metadata.ipynb
│  ├─ Projections.ipynb
│  ├─ Boosting.ipynb
│  └─ Prompt Compression.ipynb
├─ requirements.txt
├─ .env.example
└─ README.html (this file)
</code></pre>

<h2 id="contributing">Contributing</h2>
<p>Issues and PRs are welcome. Please include clear repro steps and follow the style used in existing notebooks.</p>

<h2 id="license">License</h2>
<p>MIT. See <code>LICENSE</code>.</p>

<hr/>
<p><em>Tip:</em> Start with the baseline notebook, measure, then add one optimization at a time. Ship measurable wins, not vibes.</p>
