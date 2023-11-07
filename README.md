# CFO-R-package

## CFO

### CFO.next

**Description**

Use the function to determine the dose movement based on the toxicity outcomes of the enrolled cohorts.

**usage** 
CFO.next(phi, cys, cns, alp.prior=phi, bet.prior=1-phi, cover.doses)

**Parameters**
phi: the target DLT rate
cys: the current number of DLTs observed in patients for the left, current, and right dose levels.
cns: the current number of patients for the left, current, and right dose levels.
alp.prior,bet.prior: the parameters of the prior distribution for the true DLT rate at any dose level.
                    This prior distribution is set to Beta( \code{alpha.prior}, \code{beta.prior}).
                    The default value is \code{phi} and \code{1-phi}.
cover.doses: whether the dose level (left, current and right) is over-toxic or not. 
            The value is set as 1 if the dose level is overly toxicity; otherwise, it is set to 0.
            
**details**
The CFO design determines the dose level for the next cohort by assessing evidence from the current 
dose level and its adjacent levels. This evaluation is based on odds ratios denoted as \eqn{O_k}, where 
k = L, C, R represents left, current, and right dose levels. Additionally, we define \eqn{\overline{O}_k = 1/O_k}. 
The ratio \eqn{O_C / \overline{O}_{L}} indicates the inclination for de-escalation, while \eqn{\overline{O}_C / O_R} 
quantifies the tendency for escalation. Threshold values \eqn{\gamma_L} and \eqn{\gamma_R} are chosen to 
minimize the probability of making incorrect decisions.The decision process is summarized in Table 1
of Jin and Yin (2022).
An overdose control rule is implemented to ensure patient safety. If the data suggest excessive 
toxicity at the current dose level, we exclude that level and those higher levels. Two scenarios 
lead to a decision on one side only: when the current dose is at the boundary (the first or last dose level) 
or when higher dose levels have been eliminated.

**Values**
The \code{CFO.next()} function returns a list object comprising the following elements: the target DLT 
rate ($target), the current counts of DLTs and patients for the left, current, and right dose levels ($cys and $cns), 
the decision for whether to move to the left or right dose level for the next cohort ($decision), and the 
corresponding index ($index). Specifically, 1 corresponds to de-escalation, 2 corresponds to staying at the 
current dose, and 3 corresponds to escalation.

**Author**
Jialu Fang and Wenliang Wang

**references**
Jin, H., & Yin, G. (2022). CFO: Calibration-free odds design for phase I/II clinical trials. \emph{Statistical Methods in Medical Research}, 31(6), 1051-1066.

**examples**
determine the dose level for the next cohort of new patients
cys <- c(0,1,0); cns <- c(3,6,0)
CFO.next(phi=0.2, cys=cys, cns=cns, alp.prior=0.2, bet.prior=0.8, cover.doses=c(0,0,0))

## 2dCFO

### 2dCFO_next

**Description**

Determine the dose combination for the next cohort based on the toxicity outcomes of the enrolled cohorts.

**Parameters**

target: The target DLT rate

npts: A J*K matrix (J<=K) containing the number of patients treated at each dose combination

ntox: A J*K matrix (J<=K) containing the number of patients experienced dose-limiting toxicity at each dose combination

...

**Values**

(j,k): Recommended dose combination for the next cohort

...


### 2dCFO_sim

**Description**

Conduct simulations and get operating characteristics for the 2dCFO design with customized number of iterations.

**Parameters**

target: The target DLT rate

...






