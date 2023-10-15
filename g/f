name: Run and show Java code

on:
  schedule:
    - cron: '*/1 * * * *'
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up JDK 17
        uses: actions/setup-java@v2
        with:
          java-version: 17
          distribution: 'adopt'

      - name: Run Java code in README.md file
        run: |
          java -cp . $(cat README.md | grep -Eo '`java(.*?)`' | sed -e 's/`java//g' -e 's/`//g')

      - name: Add output to README.md file
        run: |
          echo "```java
          $java -cp . $(cat README.md | grep -Eo '`java(.*?)`' | sed -e 's/`java//g' -e 's/`//g')
          ```" >> README.md

      - name: Push changes
        run: |
          git config user.name "Your Name"
          git config user.email "your_email@example.com"
          git add README.md
          git commit -m "Update README.md file with Java code output"
          git push
