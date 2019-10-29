# SDLC-Part-2-
JavaDoc 



import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.HashMap;
import java.util.List;
import java.util.Map.Entry;
import java.util.Set;

/**
 * Date October 29, 2019 This application is output text analyzer to HTML and
 * implementing JavaDoc
 * 
 * @author Luc Nguyen
 * @version 1.0
 *
 */
public class JavaDoc {

	/**
	 * Created HashMap for counting words(wordCountMap) & values.
	 */
	{
		HashMap<String, Integer> wordCountMap = new HashMap<String, Integer>();
		BufferedReader reader = null;

		/**
		 * This method created buffered reader to read file,
		 */
		try {

			reader = new BufferedReader(new FileReader("C:\\Users\\Student\\Desktop\\Shakespear.txt."));

			/**
			 * Use while loop to read each line and split each line into words for every
			 * line. Implementing for loop to iterating each word and add it in
			 * hashmap(wordCountMap). During the for loop if word already in the hasmap just
			 * updated the count and if it false inserted the words as key and one as it
			 * value.
			 */
			String currentLine = reader.readLine();
			while (currentLine != null) {
				String[] words = currentLine.toLowerCase().split(" ");
				for (String word : words) {
					if (wordCountMap.containsKey(word)) {
						wordCountMap.put(word, wordCountMap.get(word) + 1);
					} else {
						wordCountMap.put(word, 1);
					}
				}
				currentLine = reader.readLine();
			}

			/**
			 * In this method get entries of hasmap(wordCountMap) turn it into form of set.
			 * Create a list passing the entry set. Sort the list by decreasing order of
			 * values
			 * 
			 * @param e1 entry of string and integer
			 * @param e2 entry of string and integer
			 * @return returning e2 compare to e1
			 */
			Set<Entry<String, Integer>> entrySet = wordCountMap.entrySet();
			List<Entry<String, Integer>> list = new ArrayList<Entry<String, Integer>>(entrySet);
			Collections.sort(list, new Comparator<Entry<String, Integer>>() {
				@Override
				public int compare(Entry<String, Integer> e1, Entry<String, Integer> e2) {
					return (e2.getValue().compareTo(e1.getValue()));
				}
			});

			/**
			 * Display the program print out and use the for loop to get values for every
			 * word count and implementing catch exception for any false . Close the reader
			 * after the program print out.
			 */

			System.out.println("Repeated Words In Input File Are :");
			for (Entry<String, Integer> entry : list) {
				if (entry.getValue() > 1) {
					System.out.println(entry.getKey() + " : " + entry.getValue());
				}
			}
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				reader.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}

	public static void main(String[] args) {

	}
}
