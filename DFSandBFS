//Sean Stasny
//03-01-2015
//CSci 433
//Analysis of Algorithms
//I kept with The Ole Miss School of Enginnering Honor Code - my signature is on file.


package edu.olemiss.algorithms.ststasny;

import java.io.File;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.Scanner;
public class Driver2
{
	public static int[][] graph;
	static Scanner fileScanner = new Scanner(System.in);
	static Scanner consoleScanner = new Scanner(System.in);

	//Using 1 int because these are square graphs... There is a 1-to-1 relation between rows and columns.
	public static int demensions = 0; 
	static int fileNum = 0;
	static String fileName = "";
	static String playAgain = "";
	static char playAgainInitial = 'y';
	
	public static void main(String [] args) throws FileNotFoundException
	{	
		ArrayList<Integer> vertexList = new ArrayList<Integer>();
		ArrayList<Integer> iList = new ArrayList<Integer>();
		System.out.println("Welcome to Sean Stasny's <ststasny> DFS / BFS Program.");
		System.out.println();
		System.out.println("Please press enter to continue.");
		fileScanner.nextLine();
		do{
		intro();
		try
		{
			fileScanner = new Scanner(new File(fileName));
			String line1 = fileScanner.nextLine();
			String[] strArray = line1.split(" ");
			demensions = strArray.length;
			System.out.println();
			System.out.println("The demensions of the input graph adjacency matrix is: " + demensions + "x" + demensions);
			System.out.println();
			graph = new int[demensions][demensions];

			//Loop for rows.
			for(int i = 0; i <= demensions-1; i++)
			{
				//Loop for columns.
			    for(int j = 0; j <= demensions-1; j++)
			    {
			        	graph[i][j] = Integer.parseInt(strArray[j]);
			    }
			    
			    if(fileScanner.hasNextLine())
			    {
					line1 = fileScanner.nextLine();
					strArray = line1.split(" "); 
				}
			}
		fileScanner.close();

		}
		catch(FileNotFoundException e)
		{
			System.err.println("The file was not found.");
		}
		
		printGraph("~>--Adjacency Matrix--<~", "~>------------------<~", graph);
		
		DFS(vertexList, iList);
		BFS(vertexList, iList);
		
		System.out.println();
		System.out.println();
		System.out.println("Would you like to run the program again - Yes or No?");
		playAgain = consoleScanner.next();
		playAgain = playAgain.toLowerCase();
		playAgainInitial = playAgain.charAt(0);
		}while(playAgainInitial == 'y');
		System.out.println();
		System.out.println("Thank you for playing!");
	}
	
	public static void intro()
	{
		System.out.println("What sample file would you like to open? {1, 2, 3}");
		fileNum = Integer.parseInt(consoleScanner.next());
		switch(fileNum)
		{
		case 1:
			fileName = "sample1.txt";
			break;
		case 2:
			fileName = "sample2.txt";
			break;
		case 3:
			fileName = "sample3.txt";
			break;
		}
	}
	
	public static void printGraph(String title, String footer, int[][] graph)
	{
		System.out.println(title);
		//Loop for rows.
		for(int i = 0; i <= demensions-1; ++i)
		{
			System.out.print("    ");
			//Loop for columns.
		    for(int j = 0; j <= demensions-1; ++j)
		    {
		    	System.out.print(graph[i][j] + " ");
		    }
		    System.out.println();
		}
		System.out.println(footer);
	}
	
	public static void DFS(ArrayList<Integer> vertexList, ArrayList<Integer> iList)
	{
		//Index will be one off for this array... [0] = 1, [1] = 2, ... [n] = (n+1)
		boolean[] visitArray = new boolean[demensions];
		boolean[] visitArray2 = new boolean[demensions];
		ArrayList<Integer> DFSvertexList = new ArrayList<Integer>();
		ArrayList<Integer> DFSdeadEndList = new ArrayList<Integer>();

		int[][] DFStreeEdgeGraph = new int[demensions][demensions];
		int DFSnumOfComponents = 0;
		//Sets all values in visitArray to false. They will be set to true when that number is visited.
		for(int i = 0; i <= demensions-1; i++)
		{
			visitArray[i] = false;
		}
		//Initializing treeEdgeGraph to all zeros.
		//Loop for rows.
		for(int i = 0; i <= demensions-1; i++)
		{
			//Loop for columns.
		    for(int j = 0; j <= demensions-1; j++)
		    {
		        	DFStreeEdgeGraph[i][j] = 0;
		    }
		}
		//This is a for loop to go through all the nodes starting with the first node
		for(int i = 0; i <= demensions-1; i++)
		{
			//This if statement checks to see if this node has been visited yet
			if(!visitArray[i])
			{
				dfs(i, visitArray, DFSvertexList, DFSdeadEndList, DFStreeEdgeGraph, vertexList, iList, visitArray2);
				DFSdeadEndList.add(i);
				DFSnumOfComponents++;
				visitArray2[i] = true;
			}
		}
		System.out.println();
		System.out.println("DFS> Number of Connected Components: " + DFSnumOfComponents);
		System.out.print("DFS> Order> First Encountered      : ");
		for(int i : DFSvertexList)
		{
			System.out.print((i+1) + " ");
		}
		System.out.println();
		System.out.print("DFS> Order> First Dead-Ends        : ");
		for(int i : DFSdeadEndList)
		{
			System.out.print((i+1) + " ");
		}
		System.out.println();
		System.out.println();
		printGraph("~>DFS Tree Edge Graph<~", "~>---------------------<~", DFStreeEdgeGraph);
		
		int[][] crossGraph = new int[demensions][demensions];
		//Initializing crossGraph to all zeros.
		//Loop for rows.
		for(int i = 0; i <= demensions-1; i++)
		{
			//Loop for columns.
		    for(int j = 0; j <= demensions-1; j++)
		    {
		        	crossGraph[i][j] = 0;
		    }
		}
		
//		System.out.println(vertexList.toString());
//		System.out.println();
//		System.out.println(iList.toString());
		for(int i = 0; i <= iList.size()-1; i++)
		{
			crossGraph[iList.get(i)-1][vertexList.get(i)-1] = 1;
		}
		printGraph("~>DFS Back Edge Graph<~", "~>---------------------<~", crossGraph);
	}
	
	public static void dfs(int vertex, boolean[] visitArray, ArrayList<Integer> DFSvertexList, ArrayList<Integer> DFSdeadEndList, int[][] DFStreeEdgeGraph, ArrayList<Integer> vertexList, ArrayList<Integer> iList, boolean[] visitArray2)
	{
		int ver = 0;
		DFSvertexList.add(vertex);
		visitArray[vertex] = true;

		for(int i = 0; i <= demensions-1; i++)
		{
			if(graph[vertex][i] == 1)
			{
				if(!visitArray[i])
				{
					ver = i;
					DFStreeEdgeGraph[vertex][i] = 1;
					dfs(i, visitArray, DFSvertexList, DFSdeadEndList, DFStreeEdgeGraph, vertexList, iList, visitArray2);
					DFSdeadEndList.add(i);
				}

				else if(i >= vertex && i != ver)
				{
//					System.out.println("vertex: " + (vertex+1) + " i: " + (i+1) + " ver: " + (ver+1));
					vertexList.add(vertex+1);
					iList.add(i+1);
//					System.out.println((vertex + 1)+"("+ (i+1) + ")");
				}

			}
		}				
	}
	
	public static void BFS(ArrayList<Integer> vertexList, ArrayList<Integer> iList)
	{
		boolean[] visitArray = new boolean[demensions];
		boolean[] visitArray2 = new boolean[demensions];
		ArrayList<Integer> BFSvertexList = new ArrayList<Integer>();
		int[][] BFStreeEdgeGraph = new int[demensions][demensions];
		int BFSnumOfComponents = 0;
		//Initializing treeEdgeGraph to all zeros.
		//Loop for rows.
		for(int i = 0; i <= demensions-1; i++)
		{
			//Loop for columns.
		    for(int j = 0; j <= demensions-1; j++)
		    {
		        	BFStreeEdgeGraph[i][j] = 0;
		    }
		}
		for(int i = 0; i < demensions; i++)
		{
			if(!visitArray[i])
			{
				BFSvertexList.add(i);
				visitArray[i] = true;
				visitArray2[i] = true;
				bfs(i, visitArray, BFSvertexList, BFStreeEdgeGraph, vertexList, iList, visitArray2);
				BFSnumOfComponents++;
			}		
		}
		System.out.println();
		System.out.println("BFS> Number of Connected Components: " + BFSnumOfComponents);
		System.out.print("BFS> Order> First encountered      : ");
		for(int i : BFSvertexList)
		{
			System.out.print((i+1) + " ");
		}
		System.out.println();
		System.out.println();
		printGraph("~>BFS Tree Edge Graph<~", "~>---------------------<~", BFStreeEdgeGraph);
	}
	
	public static void bfs(int vertex, boolean[] visitArray, ArrayList<Integer> BFSvertexList, int[][] BFStreeEdgeGraph, ArrayList<Integer> vertexList, ArrayList<Integer> iList, boolean[] visitArray2)
	{
		for(int i = 0; i < graph.length; i++)
		{
			if(graph[vertex][i] != 0)
			{
				if(!visitArray[i])
				{
					BFStreeEdgeGraph[vertex][i] = 1;
					BFSvertexList.add(i);
					visitArray[i] = true;
				}
			}
		}
		for(int i = BFSvertexList.indexOf(vertex) + 1; i < BFSvertexList.size(); i++)
		{
			int value = BFSvertexList.get(i);
			bfs(value, visitArray, BFSvertexList, BFStreeEdgeGraph, vertexList, iList, visitArray2);
		}
	}
	
}

