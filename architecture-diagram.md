# AWS Auto Scaling Architecture

                        Internet
                            |
                    +------------------+
                    |   User Traffic   |
                    +------------------+
                            |
                ---------------------------------
                |                               |
          EC2 Instance 1                 EC2 Instance 2
                |                               |
                ---------------------------------
                            |
                    Auto Scaling Group
                            |
                    Launch Template
                            |
                    Target Tracking Policy
                     (Avg CPU 60%)

## Key Points

- Launch Template defines instance configuration
- Auto Scaling Group manages lifecycle of instances
- Scaling policy monitors CPU utilization
- Instances are automatically added or removed based on load
