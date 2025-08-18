# Book MCP Server - Tool Reference

This MCP server provides comprehensive manuscript analysis and content access tools for book writing projects. It supports markdown files and offers both basic text analysis and advanced NLP-powered features for authors, editors, and writing professionals.

## Server Overview

- **Name**: Book MCP Server
- **Purpose**: Comprehensive manuscript analysis and content access for book writing
- **Supported Files**: Markdown (.md) files
- **Total Tools**: 25 tools across 6 categories

## Tool Categories

### 1. Statistical Analysis Tools
Tools that provide statistical insights about your book project.

#### [`list_chapters()`](server.py:89)
**Purpose**: List all chapter files with enhanced metadata including titles and word counts.

**Parameters**: None

**Returns**: List of dictionaries containing:
- `filename`: Chapter filename
- `relative_path`: Path relative to book directory
- `absolute_path`: Full file path
- `chapter_title`: Extracted from first markdown header
- `word_count`: Approximate word count
- `size_bytes`: File size in bytes

**Usage Example**: "Show me all my chapters with their word counts"

---

#### [`get_book_stats()`](server.py:2036)
**Purpose**: Get overall statistics about the entire book project.

**Parameters**: None

**Returns**: Dictionary with:
- `total_chapters`: Number of markdown files
- `total_words`: Total word count across all files
- `total_size_bytes`: Total file size
- `average_words_per_chapter`: Average chapter length
- `book_directory`: Current book directory path

**Usage Example**: "What are my overall book statistics?"

---

#### [`get_chapter_length_distribution()`](server.py:1936)
**Purpose**: Analyze chapter length consistency and distribution.

**Parameters**: None

**Returns**: Dictionary with:
- `total_chapters`: Number of chapters analyzed
- `statistics`: Min, max, average, median word counts
- `distribution`: Categorization of chapters (short/medium/long)
- `consistency_analysis`: Consistency rating and recommendations
- `chapter_details`: Detailed breakdown by chapter

**Usage Example**: "Are my chapters consistently sized?"

---

#### [`get_word_frequency(min_length=3, exclude_common=True, top_n=50)`](server.py:1792)
**Purpose**: Analyze word frequency across all chapters.

**Parameters**:
- `min_length` (int): Minimum word length to include (default: 3)
- `exclude_common` (bool): Whether to exclude common English words (default: True)
- `top_n` (int): Number of top words to return (default: 50)

**Returns**: Dictionary with:
- `summary`: Total words, unique words, vocabulary richness
- `top_words`: Most frequent words with counts and percentages
- `frequency_distribution`: Words grouped by frequency ranges
- `chapter_word_distribution`: Word counts per chapter

**Usage Example**: "What are my most frequently used words?"

---

#### [`get_narrative_structure()`](server.py:1632)
**Purpose**: Analyze story structure, pacing, and narrative elements across all chapters.

**Parameters**: None

**Returns**: Dictionary with:
- `overview`: Total chapters, average length, total words
- `story_arc`: Distribution of setup/rising action/climax/resolution
- `pacing_analysis`: Dialogue, action, and tension density metrics
- `chapter_endings`: Types of chapter endings and their distribution
- `narrative_flow`: Time transitions and flow analysis
- `chapter_details`: Detailed analysis for each chapter

**Usage Example**: "How is my story structured across chapters?"

---

### 2. Content Access Tools
Tools for reading and searching specific content within your manuscript.

#### [`list_markdown_files()`](server.py:1064)
**Purpose**: List all markdown files in the book directory.

**Parameters**: None

**Returns**: List of dictionaries with:
- `filename`: File name
- `relative_path`: Path relative to book directory
- `absolute_path`: Full file path
- `size_bytes`: File size

**Usage Example**: "What files are in my book project?"

---

#### [`read_markdown_file(file_path)`](server.py:1091)
**Purpose**: Read the complete content of a specific markdown file.

**Parameters**:
- `file_path` (str): Path to the markdown file (relative or absolute)

**Returns**: Dictionary with:
- `filename`: File name
- `path`: Full file path
- `size_bytes`: Content size in bytes
- `content`: Complete file content
- `line_count`: Number of lines

**Usage Example**: "Read Chapter 5 for me"

---

#### [`search_content(query, case_sensitive=False)`](server.py:1130)
**Purpose**: Search for specific text across all markdown files.

**Parameters**:
- `query` (str): Text to search for
- `case_sensitive` (bool): Whether search should be case sensitive (default: False)

**Returns**: List of matches with:
- `filename`: File containing the match
- `relative_path`: File path relative to book directory
- `line_number`: Line number of the match
- `line_content`: Content of the matching line
- `match_query`: Original search query

**Usage Example**: "Search for all mentions of 'dragon' in my book"

---

#### [`get_file_summary(file_path, max_lines=10)`](server.py:2070)
**Purpose**: Get a preview and basic stats of a markdown file.

**Parameters**:
- `file_path` (str): Path to the file
- `max_lines` (int): Maximum number of preview lines (default: 10)

**Returns**: Dictionary with:
- `filename`: File name
- `path`: Full file path
- `total_lines`: Total number of lines
- `size_bytes`: File size
- `header_count`: Number of markdown headers
- `preview_lines`: First few lines of content
- `truncated`: Whether content was truncated

**Usage Example**: "Give me a summary of Chapter 3"

---

### 3. Advanced NLP Analysis Tools
AI-powered analysis using advanced Natural Language Processing libraries.

#### [`extract_all_characters()`](server.py:242)
**Purpose**: Automatically discover all character names using advanced NLP.

**Requirements**: spaCy library (`pipenv install spacy && python -m spacy download en_core_web_sm`)

**Parameters**: None

**Returns**: Dictionary with:
- `summary`: Total characters found, categorized by importance
- `main_characters`: Characters with >5 mentions
- `secondary_characters`: Characters with 2-5 mentions
- `isolated_characters`: Characters with only 1 mention
- `insights`: Analysis of character development and suggestions

**Usage Example**: "Who are all the characters in my book?"

---

#### [`find_isolated_characters()`](server.py:140)
**Purpose**: Quickly identify characters that appear infrequently and may need development.

**Requirements**: spaCy library

**Parameters**: None

**Returns**: Dictionary with:
- `summary`: Count of isolated and underused characters
- `isolated_characters`: Characters appearing only once
- `underused_characters`: Characters with 2-3 mentions
- `recommendations`: Specific development suggestions
- `development_priorities`: General guidance for character development

**Usage Example**: "Which characters in my book need more development?"

---

#### [`analyze_character_relationships()`](server.py:367)
**Purpose**: Analyze which characters appear together in scenes and chapters.

**Requirements**: spaCy library

**Parameters**: None

**Returns**: Dictionary with:
- `summary`: Total character pairs and relationship strength categories
- `top_relationships`: Most frequent character co-occurrences
- `isolated_characters`: Characters with no relationships
- `insights`: Relationship density and connectivity analysis

**Usage Example**: "Which characters interact most frequently?"

---

#### [`analyze_readability(chapter_path)`](server.py:495)
**Purpose**: Calculate professional readability metrics (Flesch-Kincaid, Gunning Fog, etc.).

**Requirements**: textstat library (`pipenv install textstat`)

**Parameters**:
- `chapter_path` (str): Path to the chapter file to analyze

**Returns**: Dictionary with:
- `chapter_info`: Basic chapter statistics
- `readability_scores`: Multiple readability metrics
- `text_complexity`: Reading level and assessment
- `recommendations`: Specific suggestions for improvement
- `comparison_benchmarks`: How your score compares to different fiction types

**Usage Example**: "Is Chapter 5 too complex for my target audience?"

---

#### [`comprehensive_grammar_check(chapter_path)`](server.py:612)
**Purpose**: Professional-level grammar and style checking.

**Requirements**: language-tool-python library (`pipenv install language-tool-python`)

**Parameters**:
- `chapter_path` (str): Path to the chapter file to analyze

**Returns**: Dictionary with:
- `chapter_info`: Basic file information
- `summary`: Total issues by category and overall assessment
- `issue_breakdown`: Categorized grammar, style, spelling, and punctuation issues
- `patterns`: Most common issue types and suggestions
- `recommendations`: Prioritized improvement suggestions

**Usage Example**: "What grammar errors are in Chapter 2?"

---

### 4. Semantic Search Tools (ChromaDB Integration)
Vector-based semantic search using ChromaDB for meaning-based content discovery.

#### [`connect_to_vector_db()`](server.py:2100)
**Purpose**: Connect to ChromaDB and list available collections.

**Requirements**: ChromaDB library (`pipenv install chromadb`) and existing database

**Parameters**: None

**Returns**: Dictionary with:
- `status`: Connection status
- `chroma_persist_dir`: Database directory path
- `collections`: Available collections with document counts
- `total_collections`: Number of collections

**Usage Example**: "What collections are available in my vector database?"

---

#### [`semantic_search(query, collection_name="novel_content", n_results=5)`](server.py:2141)
**Purpose**: Search content using natural language queries and vector similarity.

**Requirements**: ChromaDB library

**Parameters**:
- `query` (str): Natural language search query
- `collection_name` (str): ChromaDB collection name (default: "novel_content")
- `n_results` (int): Number of results to return (default: 5)

**Returns**: Dictionary with:
- `query`: Original search query
- `collection`: Collection searched
- `total_results`: Number of results found
- `results`: Ranked results with similarity scores and metadata

**Usage Example**: "Find all content about character development"

---

#### [`find_thematic_content(theme, collection_name="novel_content", n_results=8)`](server.py:2198)
**Purpose**: Discover content related to specific themes or concepts.

**Requirements**: ChromaDB library

**Parameters**:
- `theme` (str): Theme or concept to search for
- `collection_name` (str): ChromaDB collection name (default: "novel_content")
- `n_results` (int): Number of results to return (default: 8)

**Returns**: Dictionary with:
- `theme`: Theme searched for
- `collection`: Collection searched
- `total_matches`: Number of matches found
- `thematic_content`: Ranked thematic matches with strength scores
- `analysis`: Theme coverage assessment

**Usage Example**: "Find all content related to the theme of redemption"

---

#### [`analyze_character_relationships_semantic(character_name, collection_name="novel_content")`](server.py:2262)
**Purpose**: Use vector similarity to find character relationships beyond co-occurrence.

**Requirements**: ChromaDB library

**Parameters**:
- `character_name` (str): Name of character to analyze
- `collection_name` (str): ChromaDB collection name (default: "novel_content")

**Returns**: Dictionary with:
- `character`: Character analyzed
- `collection`: Collection searched
- `semantic_analysis`: Relationship strength and context count
- `relationship_contexts`: Relevant relationship contexts
- `insights`: Analysis of relationship development

**Usage Example**: "How does Sarah relate to other characters emotionally?"

---

#### [`check_plot_consistency_semantic(plot_element, collection_name="novel_content")`](server.py:2339)
**Purpose**: Find potentially contradictory information about plot elements.

**Requirements**: ChromaDB library

**Parameters**:
- `plot_element` (str): Plot element to check (e.g., "magic system", "timeline")
- `collection_name` (str): ChromaDB collection name (default: "novel_content")

**Returns**: Dictionary with:
- `plot_element`: Element analyzed
- `collection`: Collection searched
- `consistency_analysis`: Coverage and mention analysis
- `plot_mentions`: Relevant mentions with relevance scores
- `consistency_recommendations`: Suggestions for maintaining consistency

**Usage Example**: "Check consistency of the magic system throughout my book"

---

#### [`hybrid_character_analysis(character_name, collection_name="novel_content")`](server.py:2421)
**Purpose**: Combine semantic and exact search for comprehensive character analysis.

**Requirements**: ChromaDB library and spaCy

**Parameters**:
- `character_name` (str): Name of character to analyze
- `collection_name` (str): ChromaDB collection name (default: "novel_content")

**Returns**: Dictionary with:
- `character`: Character analyzed
- `analysis_type`: Type of analysis performed
- `semantic_insights`: Semantic relationship analysis
- `exact_mentions`: Exact text matches and locations
- `consistency_analysis`: Character consistency check
- `comprehensive_insights`: Combined analysis insights
- `recommendations`: Actionable suggestions

**Usage Example**: "Give me a complete analysis of my protagonist"

---

### 5. Editorial Feedback Tools
Tools that provide actionable editorial feedback for improving your manuscript.

#### [`analyze_writing_issues(chapter_path)`](server.py:1174)
**Purpose**: Identify specific writing problems in a chapter.

**Parameters**:
- `chapter_path` (str): Path to chapter file

**Returns**: Dictionary with:
- `passive_voice`: Instances of passive voice with suggestions
- `weak_verbs`: Overused weak verbs with counts
- `repetitive_sentence_starts`: Repeated sentence beginnings
- `overused_words`: Words appearing too frequently
- `adverb_overuse`: Excessive adverb usage
- `filler_words`: Unnecessary filler words
- `long_sentences`: Sentences that may be too complex
- `summary`: Overall assessment and statistics

**Usage Example**: "What writing issues are in Chapter 2?"

---

#### [`track_character_consistency(character_name)`](server.py:1310)
**Purpose**: Check character descriptions and traits across all chapters.

**Parameters**:
- `character_name` (str): Name of character to analyze

**Returns**: Dictionary with:
- `character_name`: Character analyzed
- `summary`: Appearance statistics and issue count
- `appearances_by_chapter`: Chapter-by-chapter breakdown
- `physical_descriptions`: Physical description mentions
- `personality_traits`: Personality trait mentions
- `dialogue_examples`: Sample dialogue
- `consistency_analysis`: Issues found and recommendations

**Usage Example**: "Check if Sarah is consistently described throughout my book"

---

#### [`check_show_vs_tell(chapter_path)`](server.py:1457)
**Purpose**: Analyze balance between showing (scenes) vs telling (summary).

**Parameters**:
- `chapter_path` (str): Path to chapter file

**Returns**: Dictionary with:
- `chapter_name`: Chapter analyzed
- `overall_analysis`: Showing/telling percentages and assessment
- `showing_elements`: Dialogue, action, sensory details counts
- `telling_elements`: Summary, exposition, abstract concepts counts
- `paragraph_breakdown`: Paragraph-by-paragraph analysis
- `recommendations`: Specific suggestions for improvement

**Usage Example**: "Is Chapter 4 too heavy on exposition?"

---

### 6. Utility Tools
General utility methods for server information and functionality.

#### [`list_methods()`](server.py:744)
**Purpose**: Show all available methods with descriptions and usage examples.

**Parameters**: None

**Returns**: Dictionary with:
- `server_info`: Server name, purpose, and configuration
- `quick_reference`: All method names and most useful tools
- `method_categories`: Detailed breakdown by category
- `usage_tips`: Getting started recommendations
- `example_workflows`: Common usage patterns and workflows

**Usage Example**: "What methods can I use?"

---

## Configuration

### Environment Variables
- `BOOK_DIRECTORY`: Directory containing your markdown files (default: current directory)
- `CHROMA_PERSIST_DIR`: ChromaDB database path (default: "./chroma_db")
- `RETRIEVAL_K`: Number of results for semantic search (default: 4)
- `EMBEDDING_MODEL`: Embedding model for ChromaDB (default: "mistral")

### Dependencies
- **Core**: Python 3.7+, FastMCP
- **NLP Features**: spaCy (`pipenv install spacy && python -m spacy download en_core_web_sm`)
- **Readability**: textstat (`pipenv install textstat`)
- **Grammar**: language-tool-python (`pipenv install language-tool-python`)
- **Semantic Search**: ChromaDB (`pipenv install chromadb`)

## Usage Tips

1. **Start with [`list_chapters()`](server.py:89)** to see your book structure
2. **Use [`search_content()`](server.py:1130)** to find character mentions or themes
3. **Run [`analyze_writing_issues()`](server.py:1174)** on chapters you're revising
4. **Check [`track_character_consistency()`](server.py:1310)** for main characters
5. **Use [`check_show_vs_tell()`](server.py:1457)** to improve scene writing
6. **Get [`get_book_stats()`](server.py:2036)** for overall progress tracking

## Example Workflows

### Chapter Revision Workflow
1. [`read_markdown_file('chapter3.md')`](server.py:1091) - Read current version
2. [`analyze_writing_issues('chapter3.md')`](server.py:1174) - Find prose problems
3. [`check_show_vs_tell('chapter3.md')`](server.py:1457) - Check scene balance
4. Revise based on feedback

### Character Development Check
1. [`hybrid_character_analysis('protagonist_name')`](server.py:2421) - Complete character analysis
2. [`analyze_character_relationships_semantic('protagonist_name')`](server.py:2262) - Semantic relationships
3. [`track_character_consistency('protagonist_name')`](server.py:1310) - Check consistency
4. Update character development based on insights

### Thematic Analysis
1. [`connect_to_vector_db()`](server.py:2100) - Check ChromaDB connection
2. [`find_thematic_content('love')`](server.py:2198) - Explore love theme
3. [`find_thematic_content('conflict')`](server.py:2198) - Explore conflict theme
4. [`semantic_search('character growth and development')`](server.py:2141) - Find development arcs
5. Strengthen weak thematic areas

### Plot Consistency Check
1. [`check_plot_consistency_semantic('magic system')`](server.py:2339) - Check world-building
2. [`check_plot_consistency_semantic('timeline')`](server.py:2339) - Check chronology
3. [`semantic_search('rules and limitations')`](server.py:2141) - Find constraint mentions
4. Fix any inconsistencies found

### Book Structure Analysis
1. [`get_book_stats()`](server.py:2036) - Overall project status
2. [`get_chapter_length_distribution()`](server.py:1936) - Check pacing
3. [`get_narrative_structure()`](server.py:1632) - Analyze story flow
4. [`semantic_search('climax and resolution')`](server.py:2141) - Find story peaks
5. Adjust structure based on insights

---

*This documentation covers all 25 tools available in the Book MCP Server. For the most up-to-date information, refer to the source code in [`server.py`](server.py).*