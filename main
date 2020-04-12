



#include <iostream>
#include<vector>
#include<algorithm>
#include <string>

using namespace std;

struct priority_Preemptive {
	string id; // Process ID
	int bt; // Burst Time
	int at; // Arrival Time
	int rmt; // remaning time
	int wt; // waiting time
	int pr; //priority


	priority_Preemptive(string i, int b, int a, int c) {
		id = i;
		bt = b;
		at = a;
		rmt = b;
		wt = 0;
		pr = c;



	}
};
void priority_pree(vector<string>&id, vector<int>&burst, vector<int>&arrival, vector<int> &start, vector<int>&priority, vector<priority_Preemptive> &v);

bool cmp(priority_Preemptive A, priority_Preemptive B) {
	if (A.pr != B.pr)
		return A.pr < B.pr;
	else
		return A.at < B.at;
}

void priority_pree_Gantt_Chart(vector<priority_Preemptive> &sr, vector<int>&ids);

float priority_pree_Waiting_time(vector<priority_Preemptive> &sr);
float priority_pree_Turn_Around(vector<priority_Preemptive> &sr);
int main()
{
	vector<priority_Preemptive> sr;
	vector<string> ids = { "p1","p2","p3","p4","p5","p6","P7" };
	vector<int>burst = { 5,2,2,3,2,2,3 };
	vector<int>arrival = { 0,1,2,15,15,17,18};
	vector<int> priority = { 2,1,3,4,4,0,1};
	vector<int> start;

	//the main function take 4 vectors
	priority_pree(ids, burst, arrival, priority, start, sr);

	for (int i = 0; i < ids.size(); i++) {
		cout << "ID : " << ids[i] << " //Time :" << burst[i] << " //Gap :" << arrival[i] << " //start: " << start[i] << endl;
	}
	//functions to calculate turn around & waiting times
	cout << "turn around time: " << priority_pree_Turn_Around(sr) << endl;
	cout << "waiting time" << priority_pree_Waiting_time(sr) << endl;


}

void priority_pree_Gantt_Chart(vector<priority_Preemptive> &sr, vector<string>&ids)
{


	int time = 0, flag = 0, num = sr.size();
	while (flag != 1)
	{
		flag = 1;

		for (int i = 0; i < sr.size(); i++) {

			if (sr[i].rmt > 0 && sr[i].at <= time) {

				//cout << "At " << time << " : process NO. :" << sr[i].id << endl;
				ids.push_back(sr[i].id);
				sr[i].rmt--;
				flag = 0;
				if (sr[i].rmt == 0) {
					num--;
				}


				for (int j = 0; j < sr.size(); j++) {
					if (j != i && sr[j].at <= time && sr[j].rmt > 0) {
						sr[j].wt++;
					}

				}
				break;


			}

		}
		if (num != 0 && flag == 1) {
			flag = 0;
			ids.push_back("-1");
			for (int j = 0; j < sr.size(); j++) {
				if (sr[j].at <= time && sr[j].rmt > 0) {
					sr[j].wt++;
				}

			}

		}
		time++;




	}
	//cout << "the processes take " << time-1 << endl;






}
float priority_pree_Waiting_time(vector<priority_Preemptive> &sr) {

	int total = 0;
	for (int i = 0; i < sr.size(); i++) {

		total += sr[i].wt;




	}

	//cout<<"avg waiting time" << (1.0*total / sr.size())<<endl;
	return (1.0*total / sr.size());


}
float priority_pree_Turn_Around(vector<priority_Preemptive> &sr) {

	int total = 0;
	for (int i = 0; i < sr.size(); i++) {

		total += sr[i].wt + sr[i].bt;




	}

	return (1.0*total / sr.size());
}


void priority_pree(vector<string>&id, vector<int>&burst, vector<int>&arrival, vector<int>&priority, vector<int> &start, vector<priority_Preemptive> &v) {
	vector<string>time_line;
	//to put the input in SRFT vector

	for (int i = 0; i < id.size(); i++) {
		v.push_back(priority_Preemptive(id[i], burst[i], arrival[i], priority[i]));
	}
	id.clear();
	burst.clear();
	arrival.clear();
	priority.clear();

	sort(v.begin(), v.end(), cmp);
	priority_pree_Gantt_Chart(v, time_line);
	string lastid = time_line[0];
	int gap = 0, time = 0;

	time_line.push_back("-1");
	for (int i = 0; i < time_line.size(); i++) {

		if (time_line[i] == lastid) {
			if (time_line[i] != "-1") {
				time++;
			}
			else if (time_line[i] == "-1") {
				gap++;
			}
		}
		else if (time_line[i] != lastid) {
			if (lastid != "-1" && time_line[i] != "-1") {
				id.push_back(lastid);
				burst.push_back(time);
				arrival.push_back(gap);
				lastid = time_line[i];
				time = 1;
				gap = 0;
			}
			else if (lastid != "-1" && time_line[i] == "-1") {
				id.push_back(lastid);
				burst.push_back(time);
				arrival.push_back(gap);
				lastid = time_line[i];
				time = 0;
				gap = 1;
			}
			else if (lastid == "-1") {
				lastid = time_line[i];
				time = 1;
			}

		}







	}




	int sta = 0;
	for (int i = 0; i < burst.size(); i++) {
		sta += arrival[i];
		start.push_back(sta);
		sta += burst[i];
	}




}
