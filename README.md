#QuizConsole

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        System.out.println("Webtoons!");
        Quiz quiz = new Quiz();
        quiz.begin();

    }
}

class Quiz
{
    void begin()
    {
        Question[] questions = new Question[5];

        questions[0] = new Question("Which is not part of PTJ universe","Lookism","Life as a Loser","Purple Hyacinth","Viral Hit", new Answer("Purple Hyacinth"));
        questions[1] = new Question("Which of following is not in the apocalypse genre","Sable Curse","The Horizon","Sweet Home","Parallel City", new Answer("Sable Curse"));
        questions[2] = new Question("Which is not part of YLAB blue sting project","Get Schooled","World is Money and Power","To Not Die","Loser Coin", new Answer("Loser Coin"));
        questions[3] = new Question("Which is included in the action genre","Hanlim Gym","A Mark Against Thee","11 of Me","Build Up", new Answer("Hanlim Gym"));
        questions[4] = new Question("Which is not included in the thriller genre","Pigpen","Chasing Tails","Melvina's Therapy","Taste of Illness", new Answer("Taste of Illness"));

        int countTotal = 0;
        int countRight = 0;
        int countWrong = 0;
        int points=0;

        for(Question q: questions)
        {
            System.out.println(q.getQuestion());
            System.out.println("A : " +q.getOption1());
            System.out.println("B : " +q.getOption2());
            System.out.println("C : " +q.getOption3());
            System.out.println("D : " +q.getOption4());

            String answer = "";

            char ans;
            System.out.println("Enter your answer");
            Scanner scan = new Scanner(System.in);
            ans = scan.next().charAt(0);

            switch(ans)
            {
                case 'a':    
                case 'A':
                    answer = q.getOption1();
                    break;
                    
                case 'B':
                case 'b':
                    answer = q.getOption2();
                    break;
                case 'C':
                case 'c':
                    answer = q.getOption3();
                    break;
                case 'D':
                case 'd':
                    answer = q.getOption4();
                    break;
                default:break;
            }
            System.out.println("Your answer : " + answer + " ");
            if(answer.equals(q.getAnswer().getAnswer()))
            {
                
                System.out.println("                  CORRECT ANSWER!                     ");
                
                countRight++;
                points=points+10;
                System.out.println("Score= "+points);
            }
            else
            {
                
                System.out.println("                  WRONG ANSWER :(                     ");
                
                countWrong++;
                System.out.println("Correct answer :"+ (q.getAnswer().getAnswer()));
            }
            System.out.println("============================================================================================");
            countTotal++;
        }

        Result result = new Result(countTotal,countRight,countWrong,points);
        result.showResult();
    }
}

class Question
{

    String question;
    String option1;
    String option2;
    String option3;
    String option4;
    Answer answer;

    public Question(String question, String option1, String option2, String option3, String option4, Answer answer) {
        this.question = question;
        this.option1 = option1;
        this.option2 = option2;
        this.option3 = option3;
        this.option4 = option4;
        this.answer = answer;
    }

    public String getQuestion() {
        return question;
    }

    public String getOption1() {
        return option1;
    }

    public String getOption2() {
        return option2;
    }

    public String getOption3() {
        return option3;
    }

    public String getOption4() {
        return option4;
    }

    public Answer getAnswer() {
        return answer;
    }
}

class Answer
{
    String answer;

    public Answer(String answer) {
        this.answer = answer;
    }

    public String getAnswer() {
        return answer;
    }
}

interface IResult
{
    void showResult();
    double showPercentage(int correctAnswers,int totalQuestions);
    
}

class Result implements IResult
{
    int totalQuestions;
    int correctAnswers;
    int wrongAnswers;
    int points;

    public Result(int totalQuestions, int correctAnswers, int wrongAnswers, int points) {
        this.totalQuestions = totalQuestions;
        this.correctAnswers = correctAnswers;
        this.wrongAnswers = wrongAnswers;
        this.points=points;
    }

    @Override
    public void showResult() {
        System.out.println("Your results!");
        System.out.println("Total Questions " + totalQuestions);
        System.out.println("Number of correct answers " + correctAnswers);
        System.out.println("Number of wrong answers " + wrongAnswers);
        System.out.println("Percentage " + showPercentage(correctAnswers,totalQuestions));
        System.out.println("Your Score= " + points);

    }

    @Override
    public double showPercentage(int correctAnswers, int totalQuestions) {
        return (double) (correctAnswers / (double)totalQuestions) * 100 ;
    }

    
}
