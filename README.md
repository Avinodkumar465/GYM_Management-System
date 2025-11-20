package com.tap.oops;

import java.util.*;


abstract class Person {
 protected String name;
 protected int age;
 protected String contact;

 public Person(String name, int age, String contact) {
     this.name = name;
     this.age = age;
     this.contact = contact;
 }

 public abstract void displayInfo();
}


class Member extends Person {
 private String membershipType;
 private int duration;

 public Member(String name, int age, String contact, String membershipType, int duration) {
     super(name, age, contact);
     this.membershipType = membershipType;
     this.duration = duration;
 }

 public String getMembershipType() {
     return membershipType;
 }

 public void setMembershipType(String membershipType) {
     this.membershipType = membershipType;
 }

 public int getDuration() {
     return duration;
 }

 public void setDuration(int duration) {
     this.duration = duration;
 }

 @Override
 public void displayInfo() {
     System.out.println("Member Name: " + name);
     System.out.println("Age: " + age);
     System.out.println("Contact: " + contact);
     System.out.println("Membership Type: " + membershipType);
     System.out.println("Duration (months): " + duration);
     System.out.println("--------------------------------");
 }
}


class Trainer extends Person {
 private String specialization;
 private double salary;

 public Trainer(String name, int age, String contact, String specialization, double salary) {
     super(name, age, contact);
     this.specialization = specialization;
     this.salary = salary;
 }

 @Override
 public void displayInfo() {
     System.out.println("Trainer Name: " + name);
     System.out.println("Age: " + age);
     System.out.println("Contact: " + contact);
     System.out.println("Specialization: " + specialization);
     System.out.println("Salary: ₹" + salary);
     System.out.println("--------------------------------");
 }
}


class GymPlan {
 private String planName;
 private double price;
 private String description;

 public GymPlan(String planName, double price, String description) {
     this.planName = planName;
     this.price = price;
     this.description = description;
 }

 public void showPlan() {
     System.out.println("Plan: " + planName + " | Price: ₹" + price);
     System.out.println("Details: " + description);
     System.out.println("--------------------------------");
 }
}


class GymManagementSystem {
 private List<Member> members = new ArrayList<>();
 private List<Trainer> trainers = new ArrayList<>();

 public void addMember(Member m) {
     members.add(m);
     System.out.println("Member added successfully!");
 }

 public void viewMembers() {
     if (members.isEmpty()) {
         System.out.println("No members found.");
     } else {
         System.out.println("----- Member List -----");
         for (Member m : members) {
             m.displayInfo();
         }
     }
 }

 public void updateMembership(String name, String newType) {
     for (Member m : members) {
         if (m.name.equalsIgnoreCase(name)) {
             m.setMembershipType(newType);
             System.out.println(" Membership updated for " + name);
             return;
         }
     }
     System.out.println(" Member not found!");
 }

 public void removeMember(String name) {
     Iterator<Member> itr = members.iterator();
     while (itr.hasNext()) {
         Member m = itr.next();
         if (m.name.equalsIgnoreCase(name)) {
             itr.remove();
             System.out.println(" Member removed successfully!");
             return;
         }
     }
     System.out.println(" Member not found!");
 }

 public void addTrainer(Trainer t) {
     trainers.add(t);
     System.out.println(" Trainer added successfully!");
 }

 public void viewTrainers() {
     if (trainers.isEmpty()) {
         System.out.println("No trainers found.");
     } else {
         System.out.println("----- Trainer List -----");
         for (Trainer t : trainers) {
             t.displayInfo();
         }
     }
 }
}


public class Main {
 public static void main(String[] args) {
     Scanner sc = new Scanner(System.in);
     GymManagementSystem gym = new GymManagementSystem();

     // Predefined Gym Plans
     GymPlan basic = new GymPlan("Basic", 999, "Access to gym equipment only");
     GymPlan premium = new GymPlan("Premium", 1999, "Includes trainer support and diet plan");
     GymPlan vip = new GymPlan("VIP", 2999, "All premium features + personal training");

     System.out.println("=== Welcome to Gym Management System ===");

     boolean running = true;

     while (running) {
         System.out.println("\n1. Add Member\n2. View Members\n3. Update Membership\n4. Remove Member\n5. Add Trainer\n6. View Trainers\n7. View Plans\n8. Exit");
         System.out.print("Enter your choice: ");
         int choice = sc.nextInt();
         sc.nextLine();

         if (choice == 1) {
             System.out.print("Enter Member Name: ");
             String name = sc.nextLine();
             System.out.print("Enter Age: ");
             int age = sc.nextInt();
             sc.nextLine();
             System.out.print("Enter Contact: ");
             String contact = sc.nextLine();
             System.out.print("Enter Membership Type (Basic/Premium/VIP): ");
             String type = sc.nextLine();
             System.out.print("Enter Duration (in months): ");
             int duration = sc.nextInt();
             gym.addMember(new Member(name, age, contact, type, duration));

         } else if (choice == 2) {
             gym.viewMembers();

         } else if (choice == 3) {
             System.out.print("Enter Member Name to Update: ");
             String updateName = sc.nextLine();
             System.out.print("Enter New Membership Type: ");
             String newType = sc.nextLine();
             gym.updateMembership(updateName, newType);

         } else if (choice == 4) {
             System.out.print("Enter Member Name to Remove: ");
             String removeName = sc.nextLine();
             gym.removeMember(removeName);

         } else if (choice == 5) {
             System.out.print("Enter Trainer Name: ");
             String tname = sc.nextLine();
             System.out.print("Enter Age: ");
             int tage = sc.nextInt();
             sc.nextLine();
             System.out.print("Enter Contact: ");
             String tcontact = sc.nextLine();
             System.out.print("Enter Specialization: ");
             String spec = sc.nextLine();
             System.out.print("Enter Salary: ");
             double sal = sc.nextDouble();
             gym.addTrainer(new Trainer(tname, tage, tcontact, spec, sal));

         } else if (choice == 6) {
             gym.viewTrainers();

         } else if (choice == 7) {
             System.out.println("----- Available Gym Plans -----");
             basic.showPlan();
             premium.showPlan();
             vip.showPlan();

         } else if (choice == 8) {
             System.out.println(" Thank you for using Gym Management System!");
             running = false;

         } else {
             System.out.println(" Invalid choice! Please try again.");
         }
     }

     sc.close();
 }
}

