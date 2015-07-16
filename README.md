# Testing
Testing out github w/ basic unity code

using UnityEngine;
using UnityEngine.UI;
using System.Collections;


public class PlayerController : MonoBehaviour {
	
	public float speed;
	private Rigidbody rb;
	private int count;
	public Text countText;
	public Text winText;
	
	//Runs a the start of the program. Initializes our stuff
	void Start()
	{
		rb = GetComponent<Rigidbody>();
		speed = 10;
		count = 0;
		SetCountText ();
		winText.text = "";
	}
	
	//Called every physics step
	//Fixed Update intervals are consistent
	//Used for regular updates such as adjusting Physics(Rigidbody) objects
	void FixedUpdate()
	{
		float moveHorizontal = Input.GetAxis("Horizontal");
		float moveVertical = Input.GetAxis("Vertical");
		
		Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
		
		rb.AddForce(movement * speed );
	}
	
	void OnTriggerEnter(Collider other)
	{
		if(other.gameObject.CompareTag("Pick Up"))
		{
			other.gameObject.SetActive(false);
			count++;
			SetCountText();
		}
	}
	
	void SetCountText()
	{
		countText.text = "Count:" + count.ToString();
		if(count >= 1)
		{
			winText.text = "YOU WIN!";
		}
	}
}
