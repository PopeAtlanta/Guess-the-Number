# Guess-the-Number
//
//  ViewController.swift
//  Guess The Number
//
//  Created by FreshMac on 9/8/17.
//  Copyright © 2017 FreshMac. All rights reserved.
//

import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var guessTextField: UITextField!
    @IBOutlet weak var guessLabel: UILabel!
    override func viewDidLoad() {
        super.viewDidLoad()
        generateRandomNumber()
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }

    func validateGuess(_ guess: Int) {
        if guess < lowerBound || guess > upperBound {
            showBoundsAlert()
        } else if guess < numberToGuess {
            guessLabel.text = "Higher! ⬆️"
        } else if guess > numberToGuess {
            guessLabel.text = "Lower! ⬇️"
        } else {
            showWinAlert()
            numberOfGuesses = 0
            generateRandomNumber()
        }
    }
    func showWinAlert() {
        let alert = UIAlertController(title: "Congrats! 🎉", message: "You won with a total of \(numberOfGuesses) guesses", preferredStyle: .alert)
        let action = UIAlertAction(title: "Play again", style: .default, handler: nil)
        alert.addAction(action)
        self.present(alert, animated: true, completion: nil)
    }
    func showBoundsAlert() {
        let alert = UIAlertController(title: "Hey!", message: "Your guess should be between 1 and 100!", preferredStyle: .alert)
        let action = UIAlertAction(title: "Got it", style: .default, handler: nil)
        alert.addAction(action)
        self.present(alert, animated: true, completion: nil)
    }
    @IBAction func submitButtonPressed(_ sender: Any) {
        if let guess = guessTextField.text {
            if let guessInt = Int(guess) {
                numberOfGuesses = numberOfGuesses + 1
                validateGuess(guessInt)

            }
        }
    }
}


let lowerBound = 1
let upperBound = 100
var numberToGuess: Int!
var numberOfGuesses = 0




func generateRandomNumber() {
    numberToGuess = Int(arc4random_uniform(100)) + 1
}
