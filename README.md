# Path_planning_RRT*

## Compile and run
    mkdir -p ~/catkin_ws/src
    cd ~/catkin_ws/src
    catkin_init_workspace
    cd ~/catkin_ws
    catkin_make
    source devel/setup.bash
    roslaunch path_finder rviz.launch

## Implement RRT* in C++
### Core codes

### Experiment results
#### Rewire without heuristic

Rewire Codes

#### Rewire with heuristic

Rewire Codes
#### Analysis

    double best_cost_before_rewire = goal_node_->cost_from_start;
    double promising_cost  = current_dist_from_new + calDist(curr_node->x, goal_node_->x)
    bool flag = promising_cost < best_cost_before_rewire

通过在Rewire的过程中加入heuristic的判断可以减少没有意义的Rewire,加快收敛速度,因为这里heuristic采用admissible的Euclidean,如果promising_cost都不能满足小于当前最优解,那么实际的path_cost也不能保证小于当前最优解.(即使前者满足,后者也不一定满足)因此减少了没有意义的Rewire,加快了收敛速度.当然因为缺少了没有意义的Rewire,整个树最后的样子看起来没有那么"整齐".

### Informed RRT*

Informed RRT* 提高了采样效率,将大范围采样转变为只在一个可能改善解的质量的范围内采样. Informed RRT* 基于RRT*,在未找到初始解时使用RRT*,当找到第一条feasible solution时,将起点和终点之间的直线距离作为焦距,将可行路径的长度作为长轴,构建一个椭圆,之后便在椭圆的内部采样.随着解的质量逐步提高,椭圆的长轴越来越短,因而导致椭圆的短轴也越来越短,最终趋向最优解.本质上来说,Informed RRT* 只是在采样方式上进行了改进,其余的和RRT* 保持一致.

#### Code
Refer to ZJU FAST Lab for modification.

#### Experiment




