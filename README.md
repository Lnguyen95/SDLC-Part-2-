# SDLC-Part-2-
JavaDoc 

	Author: Luc Nguyen
	Class: CEN 3024C
	Profesor: Gossai
	
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
 	* Date October 29, 2019 
	* This application is output text analyzer to HTML by implementing JavaDoc.
 	* @author Luc Nguyen
 	* @version 1.0
	* 
	*
	* This program will read a file and output statistic about the file. Output the most word frequencies of all words in
	* the file and sorted the most frequently used word. Display set of pair and how many time it occurred in the file. 
 	*/
	public class JavaDoc {
	{
		public static void main(String[] args) 
	{   
	// created HashMap for counting words & values
   	 
	 HashMap<String, Integer> wordCountMap = new HashMap<String, Integer>();
	 BufferedReader reader = null;
	
	try
	{
    	// created BufferedReader 
        reader = new BufferedReader(new FileReader("C:\\Users\\Student\\Desktop\\Shakespear.txt."));
         
      //Reading the first line into currentLine
        String currentLine = reader.readLine();
        while (currentLine != null)
        {   
            //splitting the currentLine into words  
            String[] words = currentLine.toLowerCase().split(" ");
            
            //Iterating each word
            for (String word : words)
            {
                //If word is already in wordCountMap, updated count
                if(wordCountMap.containsKey(word))
                {
                	wordCountMap.put(word, wordCountMap.get(word)+1);
                }
                //otherwise inserting the word as key and 1 as its value
                else
                {
                    wordCountMap.put(word, 1);
                }
            }
            //Reading next line into currentLine
            currentLine = reader.readLine();
        }
      //Getting entries of wordCountMapn into form of set
        Set<Entry<String, Integer>> entrySet = wordCountMap.entrySet();
        
      //Creating a List passing the entrySet
        List<Entry<String, Integer>> list = new ArrayList<Entry<String,Integer>>(entrySet);
        
      //Sorting the list in decreasing order of values 
        Collections.sort(list, new Comparator<Entry<String, Integer>>() 
        {
            @Override
            public int compare(Entry<String, Integer> e1, Entry<String, Integer> e2) 
            {
                return (e2.getValue().compareTo(e1.getValue()));
            }
        });

        //Printing the repeated words in input file along with their occurrences 
        System.out.println("Repeated Words In Input File Are :");
        for (Entry<String, Integer> entry : list) 
        {
        	if (entry.getValue() > 1)
            {
        		System.out.println(entry.getKey() + " : "+ entry.getValue());
            }
        }
    } 
    catch (IOException e) 
    {
        e.printStackTrace();
    }
    finally
    {
        try
        {
        	//Closing the reader
            reader.close();           
        }
        catch (IOException e) 
        {
            e.printStackTrace();
	    		}
		}
	}
