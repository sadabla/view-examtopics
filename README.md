## Explanation

This guide creates a handy, clickable HTML file from ExamTopics exam questions so you can open questions without popups or warnings.
It also uses examtopics-downloader: [https://github.com/thatonecodes/examtopics-downloader](https://github.com/thatonecodes/examtopics-downloader)

Why this guide? examtopics-downloader downloads the questions, but they are not shown in a clear overview and the discussion is not visible.

## Downoad the direct links to the questions
# Preparation

* Debian VM with Docker installed.

# Download URLs to questions

* If the Docker container has not been pulled yet:
  `docker pull ghcr.io/thatonecodes/examtopics-downloader:latest`
* Reboot
* After reboot, browse to the download location folder
* Run the following command (first change the course where you see `-p microsoft -s sc-300`):

```bash
docker run -it \
  --name examtopics-downloader \
  ghcr.io/thatonecodes/examtopics-downloader:latest \
  -p microsoft -s sc-300 \
  -save-links -o output.md

docker cp examtopics-downloader:/app/output.md .
docker cp examtopics-downloader:/app/saved-links.txt .
docker rm examtopics-downloader
```

# Convert the URL list into a clickable HTML file

* Now copy the file `saved-links.txt` into ChatGPT using the prompt below.

# ChatGPT prompt.

I have a file containing many URLs saved-links.txt
Generate a single HTML file with clickable links. Each link must open in a new tab (`target="_blank"`).

Display format:

* Heading: `Topic 1:`

  * Under it, list all questions that belong to topic 1, one question per line.
  * Each line should be: `Question X` as a clickable link to the URL.
  * The link/button must change to a different color after the question has been opened once.

You can determine the topic number and question number from the URL itself. Example: this is topic 1, question 1:
[https://www.examtopics.com/discussions/microsoft/view/51472-exam-sc-300-topic-1-question-1-discussion/](https://www.examtopics.com/discussions/microsoft/view/51472-exam-sc-300-topic-1-question-1-discussion/)

Then:

* Heading: `Topic 2:`

  * Under it, list all questions that belong to topic 2, one question per line.
  * Example for topic 2 question 1:
    [https://www.examtopics.com/discussions/microsoft/view/153521-exam-sc-300-topic-2-question-1-discussion/](https://www.examtopics.com/discussions/microsoft/view/153521-exam-sc-300-topic-2-question-1-discussion/)

Continue this pattern for all topics and questions found in the file.

## View the examtopics questions
After ChatGPT has generated the file:
* Save the HTML file
* Install the browser extension Tampermonkey 
https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=nl
* Grant the Tampermonkey extension manually permission to run userscripts, via the extension settings
* Then install this Tampermonkey script:
  [https://greasyfork.org/en/scripts/532822-examtopics-popup-remover-and-right-click-enabler](https://greasyfork.org/en/scripts/532822-examtopics-popup-remover-and-right-click-enabler)
* You can now open questions from the HTML file by clicking them without popups.
