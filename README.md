# Book MCP Server - Tool Reference

This MCP server provides comprehensive manuscript analysis and content access tools for book writing projects. It supports markdown files and offers both basic text analysis and advanced NLP-powered features for authors, editors, and writing professionals.

## Server Overview

- **Name**: Book MCP Server
- **Purpose**: Comprehensive manuscript analysis and content access for book writing
- **Supported Files**: Markdown (.md) files
- **Total Tools**: 25 tools across 6 categories

## Tool Categories

<details>
<summary><strong>1. Statistical Analysis Tools</strong> - Tools that provide statistical insights about your book project</summary>

| Tool | Description | Usage |
| --- | ----------- | ----- |
| [`list_chapters()`](server.py:89) | List all chapter files with enhanced metadata including titles and word counts | "Show me all my chapters with their word counts" |
| [`get_book_stats()`](server.py:2036) | Get overall statistics about the entire book project | "What are my overall book statistics?" |
| [`get_chapter_length_distribution()`](server.py:1936) | Analyze chapter length consistency and distribution | "Are my chapters consistently sized?" |
| [`get_word_frequency()`](server.py:1792) | Analyze word frequency across all chapters | "What are my most frequently used words?" |
| [`get_narrative_structure()`](server.py:1632) | Analyze story structure, pacing, and narrative elements across all chapters | "How is my story structured across chapters?" |

</details>

<details>
<summary><strong>2. Content Access Tools</strong> - Tools for reading and searching specific content within your manuscript</summary>

| Tool | Description | Usage |
| --- | ----------- | ----- |
| [`list_markdown_files()`](server.py:1064) | List all markdown files in the book directory | "What files are in my book project?" |
| [`read_markdown_file()`](server.py:1091) | Read the complete content of a specific markdown file | "Read Chapter 5 for me" |
| [`search_content()`](server.py:1130) | Search for specific text across all markdown files | "Search for all mentions of 'dragon' in my book" |
| [`get_file_summary()`](server.py:2070) | Get a preview and basic stats of a markdown file | "Give me a summary of Chapter 3" |

</details>

<details>
<summary><strong>3. Advanced NLP Analysis Tools</strong> - AI-powered analysis using advanced Natural Language Processing libraries</summary>

| Tool | Description | Usage |
| --- | ----------- | ----- |
| [`extract_all_characters()`](server.py:242) | Automatically discover all character names using advanced NLP | "Who are all the characters in my book?" |
| [`find_isolated_characters()`](server.py:140) | Quickly identify characters that appear infrequently and may need development | "Which characters in my book need more development?" |
| [`analyze_character_relationships()`](server.py:367) | Analyze which characters appear together in scenes and chapters | "Which characters interact most frequently?" |
| [`analyze_readability()`](server.py:495) | Calculate professional readability metrics (Flesch-Kincaid, Gunning Fog, etc.) | "Is Chapter 5 too complex for my target audience?" |
| [`comprehensive_grammar_check()`](server.py:612) | Professional-level grammar and style checking | "What grammar errors are in Chapter 2?" |

</details>

<details>
<summary><strong>4. Semantic Search Tools (ChromaDB Integration)</strong> - Vector-based semantic search using ChromaDB for meaning-based content discovery</summary>

| Tool | Description | Usage |
| --- | ----------- | ----- |
| [`connect_to_vector_db()`](server.py:2100) | Connect to ChromaDB and list available collections | "What collections are available in my vector database?" |
| [`semantic_search()`](server.py:2141) | Search content using natural language queries and vector similarity | "Find all content about character development" |
| [`find_thematic_content()`](server.py:2198) | Discover content related to specific themes or concepts | "Find all content related to the theme of redemption" |
| [`analyze_character_relationships_semantic()`](server.py:2262) | Use vector similarity to find character relationships beyond co-occurrence | "How does Sarah relate to other characters emotionally?" |
| [`check_plot_consistency_semantic()`](server.py:2339) | Find potentially contradictory information about plot elements | "Check consistency of the magic system throughout my book" |
| [`hybrid_character_analysis()`](server.py:2421) | Combine semantic and exact search for comprehensive character analysis | "Give me a complete analysis of my protagonist" |

</details>

<details>
<summary><strong>5. Editorial Feedback Tools</strong> - Tools that provide actionable editorial feedback for improving your manuscript</summary>

| Tool | Description | Usage |
| --- | ----------- | ----- |
| [`analyze_writing_issues()`](server.py:1174) | Identify specific writing problems in a chapter | "What writing issues are in Chapter 2?" |
| [`track_character_consistency()`](server.py:1310) | Check character descriptions and traits across all chapters | "Check if Sarah is consistently described throughout my book" |
| [`check_show_vs_tell()`](server.py:1457) | Analyze balance between showing (scenes) vs telling (summary) | "Is Chapter 4 too heavy on exposition?" |

</details>

<details>
<summary><strong>6. Utility Tools</strong> - General utility methods for server information and functionality</summary>

| Tool | Description | Usage |
| --- | ----------- | ----- |
| [`list_methods()`](server.py:744) | Show all available methods with descriptions and usage examples | "What methods can I use?" |

</details>

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