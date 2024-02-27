# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
```
import time
class SlidingWindowProtocol:
    def __init__(self, window_size):
        self.window_size = window_size
        self.timeout = 1
        self.buffer = []

    def send(self, frames):
        print("Sending frames:", frames)
        self.buffer.extend(frames)
        start_time = time.time()
        next_frame_to_ack = 0

        while self.buffer:
            if time.time() - start_time >= self.timeout:
                print("Timeout! Resending frames:", self.buffer[:self.window_size])
                start_time = time.time()
            else:
                if next_frame_to_ack < len(self.buffer):
                    ack_frame = self.receive_ack(next_frame_to_ack)
                    if ack_frame is not None:
                        print("Acknowledgment received for frame:", ack_frame)
                        next_frame_to_ack += 1
                        self.buffer = self.buffer[next_frame_to_ack:]
                        next_frame_to_ack = 0

    def receive_ack(self, frame_number):
        received = input("Enter '1' to simulate acknowledgment for frame {}: ".format(frame_number))
        if received == '1':
            return frame_number
        else:
            return None

if __name__ == "__main__":
    protocol = SlidingWindowProtocol(window_size=3)
    frames_to_send = ['Frame1', 'Frame2', 'Frame3', 'Frame4', 'Frame5']

    protocol.send(frames_to_send)

```
## OUPUT
![Uploading Screenshot (137).png…]()

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
