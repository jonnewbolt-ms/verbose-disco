# Step 02 - Summarize Whiteboard

- Choose one option based on whether you can access the visual board content.
- Produce the summary content required by the output contract.

## Option A: Direct lookup (text and metadata only)
Use this if you want a quick summary based on file metadata and related meeting transcript. This cannot see the actual drawings.

Prompt:
> "Summarize the key points, decisions, and architectural diagrams depicted in the whiteboard '[Whiteboard Name]'. Organize the summary by:
> 1. Core Themes: What were the main topics?
> 2. Key Decisions: What was agreed upon?
> 3. Action Items: What are the next steps and owners?
> 4. Technical Details: List any specific systems, tools, or architectures mentioned."

## Option B: Visual analysis (image export required)
Use this to analyze the actual diagrams and drawings. You must manually export the whiteboard image first.

Instructions:
1. Open the whiteboard link from Step 01.
2. Click the Settings (gear icon) in the top right.
3. Select Export image (High Resolution / PNG).
4. Save the downloaded image to the Whiteboards folder in this directory (docs/processes/post-engagement/Whiteboards).
   Recommendation: Save it as [Meeting Name].png.
5. Use the prompt below (it assumes the filename matches the meeting name).

Prompt:
> "I have saved an image export of the whiteboard from the '[Meeting Name]' meeting to Whiteboards/[Meeting Name].png. (If the file has a different name, please specify: Whiteboards/[YourFileName.png]).
>
> Please analyze the visual diagrams and text in this image.
> 1. Transcribe: List any text written on the board.
> 2. Describe Diagrams: Explain the flow, architecture, or relationships depicted in the drawings.
> 3. Synthesize: Combine this visual information with the meeting context to summarize the key technical outcomes."
