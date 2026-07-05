if user tries to create multiple pods, all pod scheudling request goes through scheduling queue
in that queue, pods are sorted based on their priority

To set the priority, we have to create priority class
higher the priority number , higher the priority

Scheduling queue (Priority sort) => Filtering ( NodeResourcesFit, NodeName, NodeUnschedulable) => Scoring (NodeResourcesFit, ImageLocality) => Binding ( DefaultBinder)


We can create multiple scheduler profiles within single scheduler