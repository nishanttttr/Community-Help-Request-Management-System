# Community-Help-Request-Management-System

import java.util.*;
import java.util.LinkedList;

public class CommunityHelpSystem {

    //1. Node for Linked List
    static class RequestNode {
        int requestId;
        String participantName;
        String request;
        RequestNode next;

        RequestNode(int requestId, String participantName, String request) {

            this.requestId = requestId;
            this.participantName = participantName;
            this.request = request;
            this.next = null;
        }
    }

    //Head of Linked List
    static RequestNode head = null;

    //add request to Linked List
    public static void addRequest(int requestId, String participantName, String request) {

        RequestNode newNode = new RequestNode(requestId, participantName, request);

        if(head == null) {
            head = newNode;
            return;
        }

        RequestNode current = head;
        while(current.next != null) {
            current = current.next;
        }
        current.next = newNode;
    }
    public static void displayRequest() {
        if(head == null) {
            System.out.println("No community request found.");
            return;
        }
        RequestNode current = head;
        System.out.println("\n===== COMMUNITY REQUEST =====");
        while(current != null) {

            System.out.println("----------------------------");
            System.out.println("Request ID : " + current.requestId);
            System.out.println("Name : " + current.participantName);
            System.out.println("Request : " + current.request);
            current = current.next;
        }
        System.out.println("-----------------------------------");
    }

    //public static void main(String[] args) {
      //  addRequest(1,"Nishant Sharma","Need help for learning digital payments");
      //  addRequest(2,"Nihal Singh","Need help for identifying fake websites");
      //  addRequest(3,"Aniket kumar","Need help for creating a strong password");
      //  displayRequest();
    //}

    //2. Queue
    //used to process request in FIFO order
    static Queue<String>requestQueue = new LinkedList<>();

    // add request to queue
    public static void addToQueue(String request) {
        requestQueue.add(request);
        System.out.println("Request added to processing queue.");
    }

    // process of next request
    public static void processRequest() {
        if(requestQueue.isEmpty()) {
            System.out.println("No requests waiting for processing.");
            return;
        }
        String request = requestQueue.poll();
        System.out.println("\n===== Processing Request =====");
        System.out.println(request);
        System.out.println("Request processed successfully.");
    }

    // display Queue
    public static void displayQueue() {
        if(requestQueue.isEmpty()) {
            System.out.println("Queue is empty.");
            return;
        }
        System.out.println("\n===== REQUEST QUEUE =====");
        for(String request : requestQueue) {
            System.out.println(request);
        }
    }

    //3 Stack
    //Used to store recently completed request
    static Stack<String>completedRequests = new Stack<>();

    // complete a request
    public static void completedRequests(String request) {
        completedRequests.push(request);
        System.out.println("Request marked as completed.");
    }

    // display completed requests
    public static void showCompletedRequests() {
        if(completedRequests.isEmpty()) {
            System.out.println("No completed request.");
            return;
        }
        System.out.println("\n===== COMPLETED REQUEST =====");

        // stack follows LIFO
        for(int i = completedRequests.size() - 1; i >= 0; i++) {
           System.out.println(completedRequests.get(i));
        }
    }

    //4. Binary Search Tree
    // Uesd to search participants IDs
    static class TreeNode {
        int participantId;
        String participantName;

        TreeNode left;
        TreeNode right;

        TreeNode(int participantId, String participantName) {
            this.participantId = participantId;
            this.participantName = participantName;
        }
    }

    static TreeNode root = null;

    //Insert participant into BST
    public static TreeNode insert(TreeNode root, int participantId, String participantName) {
        if(root == null) {
            return new TreeNode(participantId, participantName);
        }
        if(participantId < root.participantId) {
            root.left = insert(root.left, participantId, participantName);
        } else if (participantId > root.participantId) {
            root.right = insert(root.right, participantId, participantName);
        }
        return root;
    }

    //search participant in BST
    public static TreeNode search(TreeNode root, int participantId) {
        if(root == null || root.participantId == participantId) {
            return root;
        }
        if(participantId < root.participantId) {
            return search(root.left, participantId);
        }
        return search(root.right, participantId);
    }

    // inorder traversal
    public static void inorder(TreeNode root) {
        if(root == null) {
            return;
        }
        inorder(root.left);
        System.out.println("ID: " + root.participantId + "| Name: " + root.participantName);
        inorder(root.right);
    }

    // hashmap
    // store participant ID and Name
    static HashMap<Integer,String>participants = new HashMap<>();

    //Add participant
    public static void addParticipant(int id, String name) {
        if(participants.containsKey(id)) {
            System.out.println("Participant ID already exists.");
            return;
        }
        participants.put(id, name);

        //also add participant to BST
        root = insert(root, id, name);
        System.out.println("Participant registered successfully");
    }

    //search participant using HashMap
    public static void findParticipantUsingHashMap(int id) {
        if(participants.containsKey(id)) {
            System.out.println("\n ===== PARTICIPANT FOUND =====");
            System.out.println(" ID : " + id);
            System.out.println(" Name : " + participants.get(id));
        } else {
            System.out.println("Participant not found");
        }
    }

    // Display all participants
    public static void displayParticipants() {
        if(participants.isEmpty()) {
            System.out.println("No participant registered");
            return;
        }
        System.out.println("\n ===== PARTICIPANTS =====");
        for(Map.Entry<Integer, String>entry : participants.entrySet()) {
            System.out.println("ID : " + entry.getKey() + " | Name : " + entry.getValue());
        }
    }

    // Sample Data
    public static void loadSampleData() {
        //participant
        addParticipant(1,"Nishant Sharma");
        addParticipant(2,"Nihal Sharma");
        addParticipant(3,"Neha Sharma");
        addParticipant(4, "Sonali Soni");

        // Linked List Request
        addRequest(1, "Nishant Sharma", "Need help for learning digital payments");
        addRequest(2, "Nihal Sharma","Need help for identifying fake websites");
        addRequest(3, "Neha Sharma", "Need help for creating a strong password");
        addRequest(4,"Sonali Soni", "Need help for identifying fake emails");

        // queue request
        requestQueue.add("Nishant Sharma - Digital Payment Assistance");
        requestQueue.add("Nihal Sharma - Fake Websites Awareness");
        requestQueue.add("Neha Sharma - Password Security");
        requestQueue.add("Sonali Soni - Fake Email Awareness");

        //Sample completed request
        completedRequests.push("Previous Request - Digital Literacy Assistance");
    }

    // Main Method
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        loadSampleData();
        while (true) {
            System.out.println("\n=============================");
            System.out.println("COMMUNITY HELP & REQUEST MANAGEMENT SYSTEM");
            System.out.println("================================");
            System.out.println("1. View Community Requests");
            System.out.println("2. Add Community Request");
            System.out.println("3. View Request Queue");
            System.out.println("4. Process Next Request");
            System.out.println("5. Complete a Request");
            System.out.println("6. View Completed Requests");
            System.out.println("7. Search Participant using HashMap");
            System.out.println("8. Search Participant using BST");
            System.out.println("9. View Participants");
            System.out.println("10. View BST Inorder Traversal");
            System.out.println("11. Exit");
            System.out.println("\nEnter your choice: ");
            int choice = sc.nextInt();
            sc.nextLine();
            switch (choice) {
                // Linked List
                case 1:
                    displayRequest();
                    break;
                case 2:
                    System.out.print("Enter Request ID : ");
                    int requestId = sc.nextInt();
                    sc.nextLine();
                    System.out.print("Enter Participant Name: ");
                    String participantName = sc.nextLine();
                    System.out.print("Enetr Request: ");
                    String request = sc.nextLine();
                    addRequest(requestId,participantName,request);
                    System.out.print("Community request added successfully.");
                    break;

                    //queue
                case 3:
                    displayQueue();
                    break;
                case 4:
                    processRequest();
                    break;

                    //stack
                case 5:
                    System.out.print("Enter completed request description: ");
                    String completed = sc.nextLine();
                    completedRequests(completed);
                    break;
                case 6:
                    showCompletedRequests();
                    break;

                    //HashMap
                case 7:
                    System.out.print("Enter Participant ID: ");
                    int hashId = sc.nextInt();
                    findParticipantUsingHashMap(hashId);
                    break;

                    //Binary search tree
                case 8:
                    System.out.print("Enter Participant ID: ");
                    int treeId = sc.nextInt();
                    TreeNode result = search(root, treeId);
                    if(result != null) {
                        System.out.println("\n===== PARTICIPANT FOUND =====");
                        System.out.println("ID: " + result.participantId);
                        System.out.println("Name: " + result.participantName);
                    } else {
                        System.out.println("Participant not found.");
                    }
                    break;

                    //display participants
                case 9:
                    displayParticipants();
                    break;

                    // BST inorder traversal
                case 10:
                    System.out.println("\n===== BST INORDER TRAVERSAL =====");
                    inorder(root);
                    break;

                    //Exit
                case 11:
                    System.out.println("\nThank you for using the system!");
                    sc.close();
                    return;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}




Community Help &amp; Request Management System(Sample data fictional and is only there so you can demonstrate the program) | Java, DSA — Developed a Java-based system using Linked List, Queue, Stack, Binary Search Tree, and HashMap to manage community requests, process requests, track completed tasks, and search participant records. 
