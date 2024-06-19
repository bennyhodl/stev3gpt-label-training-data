# Scope of Work: AI Training Data Labeling from Podcasts

## Retrieve data
Go to this link: [training data](https://raw.githubusercontent.com/bennyhodl/stev3gpt-label-training-data/master/stev3gpt-with-source.json)

or 

```
curl -X GET https://raw.githubusercontent.com/bennyhodl/stev3gpt-label-training-data/master/stev3gpt-with-source.json >> $HOME
```
## Objective:
To label AI training data from podcasts by creating logical questions for each quote and consolidating successive quotes into coherent statements. Each consolidated quote should fit within a 512 max token length to minimize padding.

## Responsibilities:

1. **Review and Label Data:**
   - Review each provided JSON object containing podcast quotes.
   - Create a logical question for each quote based on its content.
   - The questions should be framed as if a **fan** were to ask a general question not a specific question from the podcast.

2. **Consolidate Quotes:**
   - Identify successive JSON objects that can be combined into a single coherent quote.
   - Conside that consolidated quotes should fit within a 512 max token length for consistent sized training data.

3. **Data Formatting:**
   - Maintain the original structure of the JSON objects.
   - Include the newly created question in each JSON object.
   - Update the `text` field with the consolidated quote if applicable.

## Example Data:

### Original JSON Object:
```json
{
  "id": "94b7f2b65126-0",
  "text": "Stevie Daniels Book Club. Starting now, we'll start touching on books more and more. The book is called the Monk who sold his Ferrari. And this is one of my favorite books.",
  "source": "https://youtube.com/watch?v=NlHEAQ1Zv4o&t=62s",
  "speaker": "Mike"
}
```

### Updated JSON Object:
```json 
{
  "id": "94b7f2b65126-0",
  "question": "How do I keep up with what you are reading?"
  "text": "Stevie Daniels Book Club. Starting now, we'll start touching on books more and more. The book is called the Monk who sold his Ferrari. And this is one of my favorite books.",
  "source": "https://youtube.com/watch?v=NlHEAQ1Zv4o&t=62s",
  "speaker": "Mike",
}
```

## Instructions:

1. **Creating Logical Questions:**
   - Read the `text` field of each JSON object.
   - Formulate a question that logically follows from the information given in the `text`.
   - The questions should be framed as if a **fan** were to ask a general question not a specific question from the podcast.
   - If the quote does not make any sense, or a question cannot be formulated from it, then delete it.

2. **Consolidating Quotes:**
   - Review the sequence of JSON objects.
   - If successive objects contain related content, merge their `text` fields into a single coherent quote.
   - Ensure that the merged text fits within a 512 max token length. If not, consider partial consolidation or prioritizing key information.

3. **Maintaining Data Integrity:**
   - Preserve the original `id`, `source`, and `speaker` fields.
   - Add a new field `question` with the created question for each JSON object.
   - Update the `text` field for consolidated quotes, ensuring the new text is coherent and within the specified token length.

## Deliverables:
- A `json` file of the data with an attached question.

## Quality Assurance:
- Ensure questions are clear, logical, and relevant to the quote.
- Verify that consolidated quotes are coherent and within the token limit.
- Perform a final review to ensure all JSON objects are correctly formatted and updated.

