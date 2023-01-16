---
title: Problem Solving Framework
permalink: /notes/intro-pcdit
key: notes-intro-pcdit
layout: article
nav_key: Notes
sidebar:
  nav: Notes
license: false
aside:
  toc: true
show_edit_on_github: false
show_date: false
---

## PCDIT: How to Solve Problem Computationally?

Several authors have developed approaches for guiding novice programmers through the process of problem solving. For example, in their Python textbooks, Dierbach~\cite{Dierbach2013} and Liang~\cite{liang2012a} proposed frameworks based on the steps of the software development life cycle, i.e.~analysis/requirements, design, implementation, and testing. Students are encouraged to think about the input/output requirements of the problem, design a process for obtaining the output from the input''~\cite{liang2012a}, implement it, then finally test the program on a selected set of problem instances''~\cite{Dierbach2013}. As another example, Loksa et al.~\cite{Loksa2016} proposed a framework that expands upon the design phase by encouraging students to search for analogous problems and solutions that can be applied to the one they are tackling.

These approaches share a typical characteristic in that testing is at the end of the process. Actually being able to get to the end, however, depends on the student's level of metacognitive awareness, i.e.~their ability to think on their own about the problem~\cite{Polya1945}. For students lacking metacognitive skills, previous research has highlighted the benefit of solving concrete cases \emph{before} programming~\cite{Denny2019}, as well as making the problem solving process explicit (e.g.~by using an automated assessment tool) and having them reflect on their progress~\cite{Prather-et_al18a,Prather-et_al19a}. Controlled experiments in these works revealed that students are more likely to provide a correctly implemented solution to a problem and demonstrate better metacognitive awareness.

// insert PCDIT figure

It is in this context that we developed PCDIT, a problem solving framework for novice programmers that encourages them to design/solve concrete cases before programming, and to regularly reflect using the five eponymous phases of the process (Figure~\ref{fig:pcdit_figure}): \textbf{\textcolor{MyP}{P}}roblem Definition, \textbf{\textcolor{MyC}{C}}ases, \textbf{\textcolor{MyD}{D}}esign of Algorithm, \textbf{\textcolor{MyI}{I}}mplementation, and \textbf{\textcolor{MyT}{T}}esting. A key characteristic of the framework is the `C' phase, which focuses on developing concrete cases for the problem early without actually writing any test code: students instead think about the steps at an abstract level, only mapping them down to program syntax in later phases. Another characteristic is its non-linearity: students are encouraged to engage in a reflective, case-driven, and iterative process that may feel more productive and encouraging for novices~\cite{Rist1989}. The process keeps on going until the programming task has been solved satisfactorily, meaning that the proposed answer fulfills all the requirements described in the problem statement, and can operate correctly on all test cases. Ultimately, the scaffolding of PCDIT makes the process of problem solving that many expert programmers naturally follow, but many novices do not, explicit.

## Five Steps in PCDIT Framework


The five key steps of the framework are given in Figure~\ref{fig:pcdit_figure}, and are intended to capture the problem solving process that many expert programmers naturally follow, but that novice programmers are not yet familiar with. By naming the steps and providing an acronym, we make it easier for students to reflect on where they are in the problem solving process, potentially increasing their metacognitive awareness~\cite{Prather-et_al18a,Prather-et_al19a}. It is important to note that instructors and students are encouraged to go iterate between the steps as their thinking brings clarity.

In general, the process begins with forming a \textbf{\textcolor{MyP}{P}}roblem Definition: students are asked to identify the types of inputs and outputs and summarise in natural language what it is that needs to be solved (e.g.~take a single string value as input, then return the reverse of that string as output). This step is common to many problem solving frameworks in understanding the problem and formulating it. Similar to Dierbach~\cite{Dierbach2013}, students are encouraged to provide more detail on the kind of data involved in both the input and the output and how it can be represented in the program. This step also requires students to summarise the problem in a single statement, similar to Riley's `general description'~\cite{Riley1981}.

The second phase asks students to develop concrete \textbf{\textcolor{MyC}{C}}ases, i.e.~before even thinking about the algorithm. The intention is for students to conceptualise the abstract steps from concrete inputs to outputs, helping them to generalise to an algorithm more easily in later parts of the framework. The \textbf{\textcolor{MyC}{C}}ases step is similar to the functional examples in ``How to Design Programs''~\cite{felleisen2018}. As students work on various concrete cases, they can also step back and revise their problem definitions, e.g.~adding additional information about the required data types. This step is crucial for novice programmers, many of whom do not have any existing algorithmic patterns or schemas: it may be difficult for such students to search for analogous problems as in Loksa's framework~\cite{Loksa2016}. They need to build the solution from the bottom up and this concrete \textbf{\textcolor{MyC}{C}}ases step provides a bridge to figure out the algorithmic solution in the next step. As discussed in Section~\ref{sec:related_work}, working out specific concrete cases helps students to understand the problem better, and there is evidence it helps them in implementing their solutions. We highlight that while some frameworks encourage students to write cases as part of their testing code, in PCDIT, they focus on \emph{working out the abstract steps} (e.g.~on paper) from concrete inputs to outputs.

//insert worksheet pcdit

Once students have worked on these concrete cases, they can begin the \textbf{\textcolor{MyD}{D}}esign of Algorithm phase: for each concrete input/output, we ask them to enumerate the steps they did in working out the concrete \textbf{\textcolor{MyC}{C}}ases. They are asked to look back on how they arrive at the output starting from the input. We then ask them to identify patterns in those steps and generalise them to computational steps. These steps can be written in a mix of pseudo-code and (precise) natural language---whatever the student is currently more comfortable with. This part can be iterated several times, starting with more coarse subgoals/descriptions, before refining them over the iterations, e.g.~by employing specific \emph{key words/phrases}, such as for every element in\dots, as long as\dots, or compare if\dots. Using specific keywords that sound similar to programming language syntax eases the transition from pseudo-code to actual code later. Figures~\ref{fig:annotated_worksheet}--\ref{fig:annotated_worksheet_DI} illustrate how one can take some concrete \textbf{\textcolor{MyC}{C}}ases for a problem and start to sketch an algorithm \textbf{\textcolor{MyD}{D}}esign in an intuitive (but not yet fully refined) way. (Further examples are available in Examples 1--3 of~\cite{pcdit_additional}.)

In the subsequent steps, students start to map the pseudo-code of their solution down to concrete Python in the \textbf{\textcolor{MyI}{I}}mplementation phase. In our teaching, we iterate this part of the framework with the \textbf{\textcolor{MyT}{T}}esting phase, ensuring that students are regularly testing their programs after completing every few lines of mapping. This helps to ensure novices feel motivated and productive by tackling smaller/feasible sub-problems one-by-one. In testing their code, students can use some of the \textbf{\textcolor{MyC}{C}}ases identified earlier, or propose new ones that potentially highlight the need to go back and improve other aspects of the algorithm further. The \textbf{\textcolor{MyI}{I}}mplementation step in Figure~\ref{fig:annotated_worksheet_DI} actually contains a syntax error in the list operation, illustrating the importance of going back and revising the initial implementation after the \textbf{\textcolor{MyT}{T}}esting step. 

We created a PCDIT worksheet that we share with students when teaching the framework~\cite{pcdit_additional}. Among our supplementary materials, we include fully worked examples (matrix multiplication, extraction of positive numbers of a list, etc.) using our PCDIT worksheet~\cite{pcdit_additional}.

Throughout this notes, we will emphasize the various steps of PCDIT and encourage students to work out the these steps as well when they encounter a new programming problems. 

## Novice and Expert Programmers

It is generally thought that it takes about 10 years to turn a novice into an expert programmer. It is important to highlight how expert programmers think and solve problems so that novice programmers can move towards that. In this section, we will highlight the difference between novice and expert programmers.

### Knowledge Schemas

Expert programmers efficiently organized knowledge schemas according to functional characteristics of the underlying algorithms. On the other hand, novice programmers tend to be limited to surface and superficial knowledge such as the language syntax. An example of this is that when expert programmers see a problem description, they tend to think how similar this new problems with existing problems they have solved before. Expert programmers have mental bank of large schemas of various problems and their underlying algorithm to solve these problems. On the other hand, novice programmes have not built up their solutions schemas and so limited to thinking in terms of the programming language syntax such as what statement should they use.  This indicates that novice programmers need to learn to build their solution schemas by exposing themselves to various problems and their solutions. At the same time, they need to learn to identify patterns in that problem and how they can use their existing solutions schemas to solve the new problems instead of focusing on the language syntax. 

### Strategies

Expert programmers tend to use both general problem solving strategies such as divide-and-conquer as well as specialised strategies for that particular problems. They are flexible enough to choose the strategies to employ. This owes to their existing knowledge schemas of various problems and the strategies to solve them. In this way, they tend to do a top-down, breadth-first approach to decompose and understand programs. 

On the other hand, novice programmers tend to approach programming "line by line" rather than using meaningful program "chunks" or structures. Moreover, they may have shortcomings in their planning strategies on how to reach the goal.  

### Language Constructs

Studies show that expert programmers are familiar and comfortable to use specific programming language constructs to solve the programming problems. On the other hand, novice programmers struggles with the programming language constructs. They tend to use a few common ways and syntax of the language. Novice programmers also tend to focus on the programming language constructs instead of the algorithm. They tend to think what syntax should I use instead of what kind of steps should I do to solve this problem. 

One way to help novice programmers is to strengthen their familiarity with the programming language constructrs that they use. It is important to give the understanding how the programming language works and to expose them how different constructs are used in solving different problems. Novice programmers to write code on their own using these different constructs to make them familiar. Many programming language learning is linear from one topic to another topic. However, the way our memory works require us to revisit some of these topics, exercise again and again to make one comfortable with the language. Just as learning new foreign language requires someone to make use of the language frequently, it would be the same with learning programming language. 

At the same time, learning programming language without any problem sometimes rob the context and have less motivation. The challenge is to introduce the language construct that motivates novice programmers to use them and to use them repeatedly to the point that they are comfortable and familiar with the language. 

### Testing

Expert programmers test their codes and even write the test before they write their solutions. Novice programmers tend to put testing outside of their scope. In most courses, test code are given for novice programmers. Moreover, they are not taught on how to test their code frequently in small chunks. Novice programmers are not aware when to test their code or how to test their code. 

Basic testing and debugging skills must be introduced to novice programmers from the early times. Certain concepts of programming language such as basic code invariant are useful to help them in testing their code. 

## Summary

This section introduce the readers on the problem solving framework which we adopt in this notes. We also share the difference between the expert and novice programmers in approaching a problem. Our hope is that by identifying some these differences, we can lead any novice programmers towards the direction that expert progammers have. We will highlight some of the steps in the PCDIT framework. Moreover, we will also put some highlight on how expert and novie programmers may think in approaching a particular problem examples. 