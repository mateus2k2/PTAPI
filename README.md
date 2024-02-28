<h1>Application Programming Interface</h1>
<h2>Introduction</h2>
<p>The proposed API offers a simple and efficient connection interface, implemented in C++, making it flexible for use across different platforms. The API usage involves three main steps: solution encoding and decoding, coding problem-specific components (evaluation function and movements), and connecting to the PT core implementation.</p>

<h2>Step 1: Solution Encoding</h2>
<p>In this step, a custom C++ structure is created to encode the solution. This structure extends the "solution" structure from the Problem.h file and should contain variables intended for encoding a solution to the problem. Below is an example structure for a permutation problem:</p>

<pre>
struct solPermutation : public solution {
    std::vector<int> sol;
};
</pre>

<h2>Step 2: Problem-Specific Components</h2>
<p>A C++ class is constructed to identify the problem-specific components. This class must implement the Problem interface and include functions for constructing initial solutions, generating neighboring solutions, and evaluating solutions.</p>

<pre>
class Permutation : public Problem {
public:
    Permutation(std::string filename);
    solPermutation construction();
    solPermutation neighbor(solPermutation sol);
    double evaluate(solPermutation sol);
};
</pre>

<h2>Step 3: Connecting to PT Core</h2>
<p>In this step, an object of the previously created class is instantiated, and an object of type PT is created with the desired parameters. Finally, the PT algorithm is started, and the best solution found is returned.</p>

<pre>
#include "../include/PT.h"
#include "../include/Permutation.h"

int main(int argc, char* argv[]) {
    Permutation* prob = new Permutation("F1001.txt");
    PT&lt;solPermutation&gt; algo(0.01, 1.0, 20, 200, 1000, 1, 3, 200);
    solPermutation sol = algo.start(20, prob);
    std::cout << sol.evalSol;
}
</pre>

<h2>License</h2>
<p>The API is available for download under the Creative Commons BY-NC license (CC BY-NC) at: <a href="https://creativecommons.org/licenses/">https://creativecommons.org/licenses/</a>. It can be used and adapted for non-commercial purposes, with proper credit given.</p>

