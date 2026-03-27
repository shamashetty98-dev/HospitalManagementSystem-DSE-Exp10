import java.util.*;

class Patient {
    int id;
    String name;
    String city;

    Patient(int id, String name, String city) {
        this.id = id;
        this.name = name;
        this.city = city;
    }

    @Override
    public String toString() {
        return "ID: " + id + " | Name: " + name + " | City: " + city;
    }
}

class Node {
    int data;
    Node left, right;
    Node(int item) {
        data = item;
        left = right = null;
    }
}

class HospitalBST {
    Node root;

    void insert(int data) {
        root = insertRec(root, data);
    }

    Node insertRec(Node root, int data) {
        if (root == null) return new Node(data);
        if (data < root.data)
            root.left = insertRec(root.left, data);
        else if (data > root.data)
            root.right = insertRec(root.right, data);
        return root;
    }

    void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.data + " ");
            inorder(root.right);
        }
    }
}

public class HospitalManagementSystem {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Data Structure 1: Hash Table for O(1) Search
        HashMap<Integer, Patient> patientLookup = new HashMap<>();
        // Data Structure 2: Linked List for Dynamic Updates
        LinkedList<Patient> patientList = new LinkedList<>();
        // Data Structure 3: BST for Sorted Data
        HospitalBST patientIDs = new HospitalBST();

        // Adding 20 Sample Indian Patient Records
        String[] names = {"Aarav", "Vihaan", "Aditi", "Ishani", "Sia", "Arjun", "Reyansh", "Anika", "Prisha", "Krishna",
                          "Sai", "Aavya", "Kabir", "Myra", "Aaryan", "Diya", "Vivaan", "Kiara", "Zoya", "Atharv"};

        for (int i = 0; i < 20; i++) {
            Patient p = new Patient(100 + i, names[i], "Mumbai");
            patientList.add(p);
            patientLookup.put(p.id, p);
            patientIDs.insert(p.id);
        }

        System.out.println("--- SMART HOSPITAL MANAGEMENT SYSTEM (Exp 10) ---");
        System.out.println("1. View All Patients (Linked List Traversal)");
        System.out.println("2. Search Patient by ID (Hash Table - O(1))");
        System.out.println("3. View Sorted Patient IDs (BST - Inorder Traversal)");
        System.out.println("4. Exit");

        while (true) {
            System.out.print("\nEnter choice: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.println("\n[Linked List]: Dynamic Patient Records");
                    for (Patient p : patientList)
                        System.out.println(p);
                    break;

                case 2:
                    System.out.print("\nEnter Patient ID to search: ");
                    int sid = sc.nextInt();
                    Patient found = patientLookup.get(sid);
                    if (found != null)
                        System.out.println("Found: " + found);
                    else
                        System.out.println("Not found.");
                    break;

                case 3:
                    System.out.println("\n[BST]: Sorted Patient IDs (Inorder)");
                    patientIDs.inorder(patientIDs.root);
                    System.out.println();
                    break;

                case 4:
                    System.exit(0);
            }
        }
    }
}
