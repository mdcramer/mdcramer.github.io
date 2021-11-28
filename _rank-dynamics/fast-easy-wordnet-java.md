---
title: "Fast & Easy Wordnet Java"
date: "2008-07-21"
tags: 
  - "code"
---

One of the techniques that Surf Canyon uses to determine if a search result is relevant to your query is to examine synonyms. Princeton University provides Wordnet, a structured lexicon that acts as a dictionary and thesaurus. There are a few open source Java libraries that provide a Java API to Wordnet. We tried using both JAWS and JWNL, but neither of them provided the response time that the Surf Canyon algorithm requires. JWNL supposedly provides an in-memory map version of the lexicon, but it seems that no one, including us, has been able to get it to work.

These open source libraries implement much more functionality than what we required. All we want to do is pass in a word and get back a Set of Sets of synonyms for that word. For example, if you pass in the word “fair,” the returned Sets should include the Set of synonyms that mean “evenhanded,” another Set of synonyms that mean “carnival,” and another set of synonyms that mean “attractive.”

Following is a 100-line Java class that implements this functionality very quickly. First, make sure your CLASSPATH includes the directory that contains the Wordnet database files. The class reads in 4 of the Wordnet database files. (The file names it uses are the file names from the UNIX distribution. The Windows distribution uses different file names. For example, the UNIX data.verb file is called verb.dat on Windows.)

```java
package com.surfcanyon.common;

import java.io.\*;
import java.util.\*;

/\*\*
 \* This class gets synonym sets from the Wordnet dictionary files.
 \*/
public abstract class Synonyms {
    private static final Map<String, Set<Set<String>>> WORD\_TO\_SYNOYMYM\_SETS = new HashMap<String, Set<Set<String>>>(15000);
    private static final Set<Set<String>> EMPTY\_SET = Collections.unmodifiableSet(new HashSet<Set<String>>());

    static {
        synchronized (WORD\_TO\_SYNOYMYM\_SETS) {
            load("data.adj");
            load("data.adv");
            load("data.verb");
            load("data.noun");
        }
    }

    private static void load(String path) {
        InputStream inputStream = null;
        BufferedReader reader = null;
        try {
            ClassLoader classLoader = Synonyms.class.getClassLoader();
            inputStream = classLoader.getResourceAsStream(path);
            reader = new BufferedReader(new InputStreamReader(inputStream));

            String line = null;
            while ((line = reader.readLine()) != null) {
                processLine(line);
            }
        } catch (IOException ioe) {
            throw new RuntimeException(ioe);
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException ioe) {
                }
            }

            if (inputStream != null) {
                try {
                    inputStream.close();
                } catch (IOException ioe) {
                }
            }
        }
    }

    private static void processLine(String line) {
        if ((line.length() > 17) && (line.charAt(0) == '0')) {
            // the data we want starts at the 17th character
            line = line.substring(17);

            Set<String> synonymSet = new HashSet<String>();
            StringTokenizer st = new StringTokenizer(line, " ");
            while (st.hasMoreElements()) {
                String word = st.nextToken();

                if (word.startsWith("00")) {
                    break;
                }

                if (word.length() > 2 && Character.isLetter(word.charAt(0))) {
                    synonymSet.add(word);
                }
            }

            if (synonymSet.size() > 1) {
                synonymSet = Collections.unmodifiableSet(synonymSet);
                for (String word : synonymSet) {
                    Set<Set<String>> synonymSetsForThisWord = WORD\_TO\_SYNOYMYM\_SETS.get(word);
                    if (synonymSetsForThisWord == null) {
                        synonymSetsForThisWord = new HashSet<Set<String>>();
                        WORD\_TO\_SYNOYMYM\_SETS.put(word, synonymSetsForThisWord);
                    }
                    synonymSetsForThisWord.add(synonymSet);
                }
            }
        }
    }

    public static Set<Set<String>> getSynonymSets(String word) {
        synchronized (WORD\_TO\_SYNOYMYM\_SETS) {
            Set<Set<String>> synonymSets = WORD\_TO\_SYNOYMYM\_SETS.get(word);
            return ((synonymSets != null) ? Collections.unmodifiableSet(synonymSets) : EMPTY\_SET);
        }
    }
}
```